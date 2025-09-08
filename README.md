https://dartpad.dev/819172c70640c3046828c7134e65e4ee

 Descrição Geral
 Este aplicativo em Flutter demonstra o gerenciamento de uma lista de produtos eletrônicos. Ele
 permite visualizar, adicionar e excluir produtos, utilizando navegação entre telas, formulários com
 validação e interação por meio de mensagens de feedback (SnackBars).
 
 Modelo de Dados
 A classe Produto representa um produto com três atributos principais: id, nome e preço.
 
 class Produto {
  final int id;
  final String nome;
  final double preco;
  Produto({
    required this.id,
    required this.nome,
    required this.preco,
  });
 }

  Função main() e MyApp
 O ponto de entrada do app é a função main(), que executa o widget MyApp. Este, por sua vez,
 configura o MaterialApp com título, tema e a tela inicial (ProdutoListScreen).
 
 void main() {
  runApp(const MyApp());
 }
 class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Produtos Eletrônicos',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: const ProdutoListScreen(),
      debugShowCheckedModeBanner: false,
    );
  }
 }

  Tela Principal (ProdutoListScreen)
 Esta tela exibe a lista de produtos em um ListView.builder. Cada produto é mostrado dentro de um
 Card com ícone, nome, preço e status ('Premium' ou 'Comum'). O usuário pode excluir itens (com
 confirmação) e adicionar novos produtos através do botão flutuante.
 
 class ProdutoListScreen extends StatefulWidget {
  const ProdutoListScreen({super.key});
  @override
  State<ProdutoListScreen> createState() => _ProdutoListScreenState();
 }
 class _ProdutoListScreenState extends State<ProdutoListScreen> {
  List<Produto> produtos = [
    Produto(id: 1, nome: 'Notebook', preco: 4500.00),
    Produto(id: 2, nome: 'Teclado', preco: 120.50),
    Produto(id: 3, nome: 'Mouse', preco: 80.00),
    Produto(id: 4, nome: 'Monitor', preco: 980.00),
    Produto(id: 5, nome: 'Pendrive', preco: 45.00),
  ];
  int nextId = 6;
  // Função para abrir a tela de adicionar produto
  void _abrirFormularioAdicionarProduto() async {
    final novoProduto = await Navigator.push<Produto>(
      context,
      MaterialPageRoute(
        builder: (context) => const AdicionarProdutoScreen(),
      ),
    );
    if (novoProduto != null) {
      setState(() {
        produtos.add(Produto(
          id: nextId++,
          nome: novoProduto.nome,
          preco: novoProduto.preco,
        ));
      });
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Produto "${novoProduto.nome}" adicionado!')),
      );
    }
  }

   Exclusão de Produtos
 Ao clicar no ícone de lixeira, o usuário é solicitado a confirmar a exclusão por meio de um
 AlertDialog. Se confirmado, o produto é removido da lista e uma mensagem de feedback é exibida.
 
 void _confirmarExclusao(BuildContext context, int index) {
  final produto = produtos[index];
  showDialog(
    context: context,
    builder: (ctx) => AlertDialog(
      title: const Text('Confirmar Exclusão'),
      content: Text('Deseja excluir o produto "${produto.nome}"?'),
      actions: [
        TextButton(
          onPressed: () => Navigator.pop(ctx),
          child: const Text('Cancelar'),
        ),
        TextButton(
          onPressed: () {
            setState(() {
              produtos.removeAt(index);
            });
            Navigator.pop(ctx);
            ScaffoldMessenger.of(context).showSnackBar(
              SnackBar(content: Text('Produto "${produto.nome}" excluído')),
            );
          },
          child: const Text('Excluir', style: TextStyle(color: Colors.red)),
        ),
      ],
    ),
  );
 }

  Tela de Adicionar Produto (AdicionarProdutoScreen)
Permite ao usuário cadastrar novos produtos. Contém um formulário com dois campos de entrada:
 nome do produto e preço. A validação garante que o nome não esteja vazio e que o preço seja
 numérico e válido. Após a validação, o produto é retornado à tela principal.
 class AdicionarProdutoScreen extends StatefulWidget {
  const AdicionarProdutoScreen({super.key});
  @override
  State<AdicionarProdutoScreen> createState() => _AdicionarProdutoScreenState();
 }
 class _AdicionarProdutoScreenState extends State<AdicionarProdutoScreen> {
  final _formKey = GlobalKey<FormState>();
  final _nomeController = TextEditingController();
  final _precoController = TextEditingController();
  void _salvarProduto() {
    if (_formKey.currentState!.validate()) {
      final nome = _nomeController.text;
      final preco = double.parse(_precoController.text);
      final novoProduto = Produto(id: 0, nome: nome, preco: preco);
      Navigator.pop(context, novoProduto);
    }
  }
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Adicionar Produto')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                controller: _nomeController,
                decoration: const InputDecoration(labelText: 'Nome do Produto'),
                validator: (value) => value == null || value.isEmpty
                    ? 'Informe o nome do produto'
                    : null,
              ),
              TextFormField(
                controller: _precoController,
                decoration: const InputDecoration(labelText: 'Preço (R\$)'),
                keyboardType: TextInputType.numberWithOptions(decimal: true),
                validator: (value) {
                  if (value == null || value.isEmpty) return 'Informe o preço';
                  final parsed = double.tryParse(value);
                  if (parsed == null || parsed < 0) return 'Informe um valor válido';
                  return null;
                },
              ),
              const SizedBox(height: 20),
              ElevatedButton(
                onPressed: _salvarProduto,
                child: const Text('Salvar'),
              )
            ],
          ),
        ),
      ),
    );
  }
 }

  Conclusão
 Este projeto demonstra conceitos essenciais do Flutter, incluindo: - Separação de lógica em
 widgets com estado e sem estado. - Uso de formulários com validação. - Navegação entre telas
 com Navigator. - Manipulação dinâmica de listas. - Exibição de feedback para o usuário com
 SnackBars. Assim, serve como base sólida para aplicações mais complexas envolvendo CRUD

 
