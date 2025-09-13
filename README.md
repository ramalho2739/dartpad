De preferencia para testar no computador 

Parte 1 
https://dartpad.dev/ebf53a6c8d4deaa6f473f843460b69e2

parte 2
https://dartpad.dev/0f3871204647ba2614571ae6b888feb2

Parte 3 
https://dartpad.dev/819172c70640c3046828c7134e65e4ee

Gabriel Cordeiro Alves 
Caio de vasconcelos Ramalho
Diogenes Lopes Dias de Souza

-----------------------------------------------------------------------------------------------------------------------------PARTE 1------------------------------------------------------------------------------------------------------------------------------------
Descrição Geral
 Este código em Dart define uma classe Produto e demonstra como manipular listas de objetos. Ele separa os produtos em duas categorias: Premium (preço acima de R$ 50) e Comum (preço menor ou igual a R$ 50). Além disso, exibe os produtos ordenados de forma organizada no console.
 
 Definição da Classe Produto
 A classe Produto contém três atributos: id, nome e preco. Todos são obrigatórios e fornecidos pelo construtor.
 
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
 
 Função main()
 A função principal cria uma lista de produtos e depois aplica filtros e ordenações para classificar os itens em Premium e Comuns.
 
 void main() {
  List<Produto> produtos = [
    Produto(id: 1, nome: 'Notebook', preco: 4500.00),
    Produto(id: 2, nome: 'Teclado', preco: 120.50),
    Produto(id: 3, nome: 'Mouse', preco: 80.00),
    Produto(id: 4, nome: 'Monitor', preco: 980.00),
    Produto(id: 5, nome: 'Pendrive', preco: 45.00),
  ];
 }
 
 Filtragem de Produtos Premium
 Aqui são selecionados apenas os produtos com preço maior que R$ 50. Eles são classificados em ordem decrescente de preço para exibição.
 
 List<Produto> produtosPremium = produtos
    .where((produto) => produto.preco > 50)
    .toList()
  ..sort((a, b) => b.preco.compareTo(a.preco));
 Filtragem de Produtos Comuns
 Seleciona os produtos com preço menor ou igual a R$ 50.
 List<Produto> produtosComuns =
    produtos.where((produto) => produto.preco <= 50).toList();
    
Exibição no Console
 Os produtos são exibidos no console com um título geral e marcadores diferentes para Premium e Comuns.
 
 print('=== Lista de Produtos ===');
 for (var produto in produtosPremium) {
  print(' Produto Premium: ${produto.nome} (R\$${produto.preco})');
 }
 for (var produto in produtosComuns) {
  print('• Produto comum: ${produto.nome} (R\$${produto.preco})');
 }
 
 Conclusão
 Este código demonstra conceitos básicos de programação em Dart: definição de classes, uso de listas, filtros com where(), ordenação com sort() e exibição de dados formatados no console. Serve como exemplo didático para iniciantes.
 
-----------------------------------------------------------------------------------------------------------------------------PARTE 2------------------------------------------------------------------------------------------------------------------------------------
 Descrição Geral
 Este aplicativo em Flutter exibe uma lista de produtos eletrônicos separados em duas categorias:
 Produtos Premium (preço maior ou igual a R$ 50) e Produtos Econômicos (preço abaixo de R$50). Cada produto é mostrado com um identificador (ID), nome e preço, utilizando widgets como ListView, ListTile e CircleAvatar.
 
 Classe Produto
 Define a estrutura de um produto com três atributos principais: id, nome e preco. Utiliza construtor com parâmetros obrigatórios.
 
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
 
 Função main()
 O ponto de entrada do app chama o método runApp() para iniciar a aplicação Flutter, carregando o widget MyApp.
 
 void main() {
  runApp(MyApp());
 }

 Classe MyApp
 MyApp é um StatelessWidget que define a interface principal. Ela contém uma lista estática de produtos e organiza a tela principal usando MaterialApp e Scaffold.
 
 class MyApp extends StatelessWidget {
  final List<Produto> produtos = [
    Produto(id: 1, nome: 'Notebook', preco: 4500.00),
    Produto(id: 2, nome: 'Teclado', preco: 120.50),
    Produto(id: 3, nome: 'Mouse', preco: 80.00),
    Produto(id: 4, nome: 'Monitor', preco: 980.00),
    Produto(id: 5, nome: 'Pendrive', preco: 45.00),
  ];
  @override
  Widget build(BuildContext context) {
    // ...
  }
 }
 Filtragem dos Produtos
 Dentro do método build(), os produtos são filtrados em duas categorias: - produtosEconomicos: preço menor que R$ 50. - produtosPremium: preço maior ou igual a R$ 50.
 
 final produtosEconomicos = produtos.where((p) => p.preco < 50.0).toList();
 final produtosPremium = produtos.where((p) => p.preco >= 50.0).toList();[
 
 Exibição da Lista
 A interface exibe os produtos em duas seções dentro de um ListView: - Produtos Premium: aparecem com fundo dourado e ícone de estrela. - Produtos Econômicos: aparecem apenas com ID e informações básicas.
 
 body: ListView(
  children: [
    if (produtosPremium.isNotEmpty)
      Padding(
        padding: const EdgeInsets.all(8.0),
        child: Text(
          'Produtos Premium',
          style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
        ),
      ),
    ...produtosPremium.map((produto) => ListTile(
          leading: CircleAvatar(
            backgroundColor: Colors.amber[700],
            child: Text(produto.id.toString()),
          ),
          title: Text(produto.nome),
          subtitle: Text('R\$ ${produto.preco.toStringAsFixed(2)}'),
          trailing: Icon(Icons.star, color: Colors.amber),
        )),
    if (produtosEconomicos.isNotEmpty)
      Padding(
        padding: const EdgeInsets.all(8.0),
        child: Text(
          'Produtos Econômicos',
          style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
        ),
      ),
    ...produtosEconomicos.map((produto) => ListTile(
          leading: CircleAvatar(
            child: Text(produto.id.toString()),
          ),
          title: Text(produto.nome),
          subtitle: Text('R\$ ${produto.preco.toStringAsFixed(2)}'),
        )),
  ],
 )
 Conclusão
 Este código exemplifica conceitos importantes do Flutter: uso de StatelessWidget, organização de layout com Scaffold e ListView, aplicação de filtros em listas, e personalização de ListTile. É um exemplo didático para exibir dados categorizados em uma interface simples e organizada
-----------------------------------------------------------------------------------------------------------------------------PARTE 3------------------------------------------------------------------------------------------------------------------------------------
 Descrição Geral
 Este aplicativo em Flutter demonstra o gerenciamento de uma lista de produtos eletrônicos. Ele permite visualizar, adicionar e excluir produtos, utilizando navegação entre telas, formulários com validação e interação por meio de mensagens de feedback (SnackBars).
 
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
 O ponto de entrada do app é a função main(), que executa o widget MyApp. Este, por sua vez, configura o MaterialApp com título, tema e a tela inicial (ProdutoListScreen).
 
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
 Esta tela exibe a lista de produtos em um ListView.builder. Cada produto é mostrado dentro de um Card com ícone, nome, preço e status ('Premium' ou 'Comum'). O usuário pode excluir itens (com confirmação) e adicionar novos produtos através do botão flutuante.
 
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
 Ao clicar no ícone de lixeira, o usuário é solicitado a confirmar a exclusão por meio de um AlertDialog. Se confirmado, o produto é removido da lista e uma mensagem de feedback é exibida.
 
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
 nome do produto e preço. A validação garante que o nome não esteja vazio e que o preço seja numérico e válido. Após a validação, o produto é retornado à tela principal.
 
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
 Este projeto demonstra conceitos essenciais do Flutter, incluindo: - Separação de lógica em widgets com estado e sem estado. - Uso de formulários com validação. - Navegação entre telas
 com Navigator. - Manipulação dinâmica de listas. - Exibição de feedback para o usuário com
 SnackBars. Assim, serve como base sólida para aplicações mais complexas envolvendo CRUD

 
