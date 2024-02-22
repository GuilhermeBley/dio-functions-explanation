# Funções em C#

Nesse artigo vai ser apresentado como podem ser utilizadas e o que são as funções na linguagem C#.
Primeiramente, deve ser explicado o que são as funções, sendo elas basicamente blocos de código que realizam uma atividade específica e podem ser reutilizados em diferentes partes de uma aplicação.
Agora que foi apresentado um _overview_ do que são as funções, podemos agora entrar um pouco mais afundo e explicar, aplicar e exemplificar alguns dos mais comuns usos de funções no C#.

## Métodos

Métodos são um tipo de função, que são representados por blocos de código dentro de uma classe, sua sintaxe é definida pelo nível de acesso, assinaturas opicionais, tipo do retorno, nome do método, parâmetro opcional tipado, seus respectivos parâmetros, e por fim, a ação que o método vai realizar ao ser executado.

```csharp
public void NomeDoMetodo(string param1, string param2)
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

## Delegados

Outro tipo de função muito comum utilizada no C# são os _delegates_ (delegados), eles são divididos em duas partes, sendo a primeira a _Action_ (`Action<...>`) e a _Func_ (`Func<..., TRetorno>`). A maneira de escrita e implementação se diferem dos métodos, porém, seu funcionamento interno é semelhante.
Os _delegates_ como já mencionado anteriormente, possuí diversas diferenças dos métodos, como por exemplo as assinaturas, nele não são aplicados nenhuma delas explicitamente, porém, em contra-mão, possuí semelhanças, como conter um bloco de código, um retorno e também pode ser nomeado, como pode ser visto no seguinte exemplo:

```csharp
// Semelhante ao método void
Action acao = () => {
    // faça algo
};

// Semelhante à um método com retorno
Func<string> acaoComRetorno = () => {
    return "Retorno obrigatório";
};
```

Como visto no exemplo, sua sintaxe acaba sendo pouco menos intuitiva que os métodos, já que o _delegate_ pode ser armazendo em uma variavel, propriedade, etc. 

### Action

Começando pela _Action_, aproveitando o assunto anterior de métodos, podemos de forma simples interpreta-la como um  método de retorno `void`, 

### Func

### Utilização

Esse tipo de função _delegate_ acaba sendo extremamente útil e amplamente utilizado na linguagem C#, já que ela possuí a capacidade de armazenar um bloco de código, por se tratar de ser um objeto, ele pode ser instanciado, permitindo que possa ser executado a qualquer momento ou passado adiante.
Um dos casos de uso mais comum são em classes de configuração, como por exemplo, o famoso Entity Framework, em sua implementação podemos ver que é utilizado uma _Action_.

```csharp
builder.Services.AddDbContext<SeuDbContext>(configuracao =>
{
    // Utilizando uma Action para configuração.
    // Parâmetro 'configuracao' passa um objeto editável que será
    // executado posteriormente.
});
```

Referências: 
    Methods: https://learn.microsoft.com/pt-br/dotnet/csharp/programming-guide/classes-and-structs/methods
    Delegados: https://www.freecodecamp.org/news/action-and-func-delegates-in-c-sharp/

