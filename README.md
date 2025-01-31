import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de FutureBuilder'),
        ),
        body: Center(
          child: FutureExample(),
        ),
      ),
    );
  }
}

class FutureExample extends StatelessWidget {
  // Função que simula um delay (ex: carregando dados de uma API)
  Future<String> fetchData() async {
    await Future.delayed(Duration(seconds: 3)); // Simulando uma espera de 3 segundos
    return 'Dados carregados com sucesso!';
  }

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<String>(
      future: fetchData(), // Passando o futuro para o FutureBuilder
      builder: (context, snapshot) {
        // Verificando o estado do futuro
        if (snapshot.connectionState == ConnectionState.waiting) {
          return CircularProgressIndicator(); // Exibindo um indicador de carregamento enquanto espera
        } else if (snapshot.hasError) {
          return Text('Erro: ${snapshot.error}'); // Caso haja erro na operação
        } else if (snapshot.hasData) {
          return Text(snapshot.data!); // Exibindo os dados quando a operação for bem-sucedida
        } else {
          return Text('Sem dados'); // Caso não tenha dados
        }
      },
    );
  }
}
