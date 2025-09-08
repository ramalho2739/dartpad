import 'package:flutter/material.dart';

// Modelo de dados
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

void main() {
  runApp(const MyApp());
}

// App principal
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

// Tela principal com estado e interatividade
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

  // Ir para a tela de adicionar produto
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
        SnackBar(
          content: Text('Produto "${novoProduto.nome}" adicionado!'),
          duration: const Duration(seconds: 2),
        ),
      );
    }
  }

  // Confirmar exclusão
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
                SnackBar(
                  content: Text('Produto "${produto.nome}" excluído'),
                  duration: const Duration(seconds: 2),
                ),
              );
            },
            child: const Text(
              'Excluir',
              style: TextStyle(color: Colors.red),
            ),
          ),
        ],
      ),
    );
  }

  // Construção da interface
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Produtos Eletrônicos'),
      ),
      body: ListView.builder(
        itemCount: produtos.length,
        itemBuilder: (context, index) {
          final produto = produtos[index];
          final isPremium = produto.preco > 50;

          return Card(
            margin: const EdgeInsets.symmetric(horizontal: 12, vertical: 6),
            elevation: 3,
            child: ListTile(
              leading: Icon(
                isPremium ? Icons.star : Icons.electrical_services,
                color: isPremium ? Colors.amber : Colors.grey,
              ),
              title: Text(produto.nome),
              subtitle: Text('R\$ ${produto.preco.toStringAsFixed(2)}'),
              trailing: Row(
                mainAxisSize: MainAxisSize.min,
                children: [
                  Text(
                    isPremium ? 'Premium' : 'Comum',
                    style: TextStyle(
                      color: isPremium ? Colors.green : Colors.black,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  IconButton(
                    icon: const Icon(Icons.delete, color: Colors.red),
                    tooltip: 'Excluir',
                    onPressed: () => _confirmarExclusao(context, index),
                  ),
                ],
              ),
            ),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _abrirFormularioAdicionarProduto,
        child: const Icon(Icons.add),
        tooltip: 'Adicionar Produto',
      ),
    );
  }
}

// Página de formulário para adicionar produto
class AdicionarProdutoScreen extends StatefulWidget {
  const AdicionarProdutoScreen({super.key});

  @override
  State<AdicionarProdutoScreen> createState() =>
      _AdicionarProdutoScreenState();
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
  void dispose() {
    _nomeController.dispose();
    _precoController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Adicionar Produto'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                controller: _nomeController,
                decoration: const InputDecoration(labelText: 'Nome do Produto'),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Informe o nome do produto';
                  }
                  return null;
                },
              ),
              TextFormField(
                controller: _precoController,
                decoration: const InputDecoration(labelText: 'Preço (R\$)'),
                keyboardType: TextInputType.numberWithOptions(decimal: true),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Informe o preço';
                  }
                  final parsed = double.tryParse(value);
                  if (parsed == null || parsed < 0) {
                    return 'Informe um valor válido';
                  }
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

