# Funções em C#

Nesse artigo vai ser apresentado como podem ser utilizadas e o que são as funções na linguagem C#.
Primeiramente, deve ser explicado o que são as funções, sendo elas basicamente blocos de código que realizam uma atividade específica e podem ser reutilizados em diferentes partes de uma aplicação.
Agora que foi apresentado um _overview_ do que são as funções, podemos agora entrar um pouco mais afundo e explicar, aplicar e exemplificar alguns dos mais comuns usos de funções no C#.

## Métodos

Métodos são blocos de código dentro de uma classe, sua sintaxe é definida pelo nível de acesso, assinaturas opicionais, tipo do retorno, nome do método, parâmetro opcional tipado, e por fim, seus respectivos parâmetros.

```csharp
public void MyMethodName(string param1, string param2)
{
    // your code here
}
```

Agora vamos ver o que é especificamente cada um desses itens mencionados.

### Assinaturas dos métodos

- public
- internal
- protected
- private

![Encapsulamento](https://github.com/GuilhermeBley/dio-functions-explanation/assets/69880922/53a9b303-d148-467c-9fa2-68fa1985aad6)

Os métodos também podem ter outros tipos de assinaturas opicitonais, como por exemplo:

- abstract
- virtual
- async
- sealed
- static
  Métodos com assinatura `static` não compartilham do contexto da classe, como o próprio nome diz, eles são estáticos e não tem um 'estado'.
  
### Retornos

- void
- object

### Nomenclatura do método

### Parâmetros tipados e não tipados

### Utilização

- Utilização sem retorno
- Utilização com retorno
- Utilização com parâmetros
- Utilização com parâmetros tipados
  Falar sobre `System.Text.Json.JsonSerializar`
  
- Utilização abstract e virtual
- Utilização sealed
- Utilização static

Referências: https://learn.microsoft.com/pt-br/dotnet/csharp/programming-guide/classes-and-structs/methods

