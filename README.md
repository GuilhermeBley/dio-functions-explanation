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

Começando pela _Action_, aproveitando o assunto anterior de métodos, podemos de forma simples interpreta-la como um  método de retorno `void`, sendo assim, não é necessário realizar nenhum tipo de retorno dentro do bloco de código.
Os parâmetros dos métodos podem ser utilizados da mesma forma, diferindo somente a maneira como devem ser passados, como pode ser visto no seguinte exemplo:


```csharp
Action<string, int> acao = (parametro1, parametro2) => {
    // faça algo
};
```
O `parametro1` é uma `string` e o `parametro2` é um `int`, como pode ser visto no tipo da variável `Action<string, int>`, esses parâmetros seguem a mesma ordem que os argumentos tipados colocados na _Action_, podendo comportar até 16 parâmetros na versão _.net core 6_.

### Func

Como mencionado anteriormente, a _Func_ é igual à um método com retorno, e segue a mesma lógica de uma _Action_ também, podendo receber parâmetros e ser instânciavel.

```csharp
Func<int, int, int> someDoisNumeros = (numero1, numero2) => {
    return numero1 + numero2;
};
```

Sobre os argumentos tipados da _Func_, é importante salientar que o primeiro à direita sempre vai ser o retorno que ela vai ter, sendo assim, um argumento tipado obrigatório deste objeto. Também é importante mencionar que uma _Func_ deve sempre retornar um valor, gerando um erro em qualquer um dos casos mencionados anteriormente:

```csharp
// Gera o erro CS0305 por não definir um retorno
Func funcao = () => {
    
};

// Gera o erro CS1643 por não efetuar nenhum retorno
Func<int> funcao = () => {
    
};
```

### Utilização

Esse tipo de função _delegate_ acaba sendo extremamente útil e amplamente utilizado na linguagem C#, já que ela possuí a capacidade de armazenar um bloco de código, por se tratar de ser um objeto, ele pode ser instanciado, permitindo que possa ser executado a qualquer momento ou passado adiante.
Após realizar a instancição de uma função _delegate_ a execução contida no bloco deve ser feita explicitamente, a maneira mais comum de realizar essa execução é a utilização do método `Invoke` ou apenas colocar o parenteses após o nome da variavel, que está contido em qualquer tipo de _delegate_:

```csharp
Action<string> acao = (parametro1) => {
    // faça algo
};


Func<int, int, int> someDoisNumeros = (numero1, numero2) => {
    return numero1 + numero2;
};

var parametro1 = "minha string";

acao.Invoke(parametro1);
acao(parametro1);

int numeroParaSoma1 = 1, numeroParaSoma2 = 1;

var valorDoRetorno = someDoisNumeros(numeroParaSoma1, numeroParaSoma2); // valorDoRetorno = 2
valorDoRetorno = someDoisNumeros(numeroParaSoma1, numeroParaSoma2); // valorDoRetorno = 2
```

Um dos casos de uso mais comum são em classes de configuração, como por exemplo, o famoso Entity Framework, em sua implementação podemos ver que é utilizado uma _Action_.

```csharp
builder.Services.AddDbContext<SeuDbContext>(configuracao =>
{
    // Utilizando uma Action para configuração.
    // Parâmetro 'configuracao' passa um objeto editável que será
    // coletado posteriormente.
});
```

### Importância das funções no C#

Referências: 
    Methods: https://learn.microsoft.com/pt-br/dotnet/csharp/programming-guide/classes-and-structs/methods
    Delegados: https://www.freecodecamp.org/news/action-and-func-delegates-in-c-sharp/

