# Funções em C#

Nesse artigo vai ser apresentado como podem ser utilizadas e o que são as funções na linguagem C#. <br/>
As funções são basicamente blocos de código que realizam uma atividade específica e podem ser reutilizados em diferentes partes de uma aplicação, podendo elas ser utilizadas extensivamente para dividir código, separar funcionalidades e especificar ações. <br/>
Agora que foi apresentado um _overview_ do que são as funções, podemos agora entrar um pouco mais afundo e explicar, aplicar e exemplificar alguns dos mais comuns usos de funções no C#. <br/>

## Métodos

Métodos são um tipo de função mais comum, eles são representados por blocos de código dentro de uma classe, sua sintaxe é definida pelo nível de acesso, assinaturas opicionais, tipo do retorno, nome do método, parâmetro opcional tipado, seus respectivos parâmetros, e por fim, a ação que o método vai realizar ao ser executado. <br/>

```csharp
public void NomeDoMetodo(string param1, string param2)
{
    // your code here
}
```

Agora vamos ver o que é especificamente cada um desses itens mencionados.

### Assinaturas dos métodos

Para iniciar a aplicação de um método, deve-se primeiramente colocar seu nível de visibilidade, sendo eles quatro, `public`, `internal`, `protected` e `private`, estando em uma ordem do mais vísivel para o menos. Isso acaba sendo um recurso fundamental na linguagem de programação, pois por conta disso é possível controlar o acesso aos membros de uma classe. <br/>
#### public
    Método pode ser acessado de qualquer local ou projeto.

```csharp
namespace Projeto2
{
    using Projeto1;

    public static class Program
    {
        public static void Main()
        {
            // Consigo acessar por aqui
            new ExemploPublico().MetodoPublico();
        }
    }
}

namespace Projeto1
{
    public static class Program
    {
        public class ExemploPublico
        {
            public void MetodoPublico()
            {
                // Faça algo
            }
        }
    }
}
```
  
#### internal <br/>
    Método pode ser acessado de qualquer local dentro do próprio projeto (mesmo _Assembly_).
```csharp
namespace Projeto2
{
    using Projeto1;

    public static class Program
    {
        public static void Main()
        {
            // Gera erro CS0122 por conta de ser inacessível
            new ExemploInterno().MetodoInterno();
        }
    }
}

namespace Projeto1
{
    public static class Program
    {
        public static void Main()
        {
            
            // Consigo acessar por aqui
            new ExemploPublico().MetodoInterno();
        }

        public class ExemploInterno
        {
            internal void MetodoInterno()
            {
                // Faça algo
            }
        }
    }
}
```

Obs. Exemplo de método `internal` e `public` anterior simula `projeto1` e `projeto2` em diferentes projetos, e não no mesmo arquivo.

#### protected <br/>
    Método pode ser acessado somente de dentro da classe ou caso tenha uma herança.

```csharp
public static void Main()
{
    // Gera erro CS0122 em qualquer uma das classes por conta de ser inacessível
    new ExemploProtectedHeranca().MetodoProtegido();
    new ExemploProtected().MetodoProtegido();
}

public class ExemploProtectedHeranca : ExemploProtected
{
    public void MetodoPublico()
    {
        MetodoProtegido(); // Consigo acessar por aqui
    }
}

public class ExemploProtected
{
    protected void MetodoProtegido()
    {
        // Faça algo
    }
}
```
  
#### private <br/>
    Método pode ser acessado somente de dentro da classe.

```csharp
public static void Main()
{
    // Gera erro CS0122 por conta de ser inacessível
    new ExemploPrivado().MetodoPrivado();
}

public class ExemploPrivado
{
    public void MetodoPublico()
    {
        MeuMetodoPrivado(); // Consigo acessar por aqui
    }

    private void MetodoPrivado()
    {
        // Faça algo
    }
}
```
Como pode ser visto nos exemplos, os modificadores de acesso tem um imenso poder dentro do código, através das palavras reservadas `private`, `public`, `internal` e `protected` pode ser controlado quem consegue acessar os métodos de uma classe, tendo níveis para cada um e gerando exceções no caso de descumprimento da norma. Uma maneira mais simples de entender pode ser vista na seguinte imagem, onde cada nível demonstra uma camada a mais de acessibilidade:

![Encapsulamento](https://github.com/GuilhermeBley/dio-functions-explanation/assets/69880922/53a9b303-d148-467c-9fa2-68fa1985aad6)

Essas assinaturas são fundamentais para controlar o acesso aos métodos de uma classe, promovendo maior segurança, modularidade e manutenibilidade do código em projetos C#.

Além disso, os métodos também podem ter outros tipos de assinaturas opicitonais, como por exemplo:

#### abstract, virtual e sealed
Estes recursos de assinatura são utilizados em casos de herança de classes, podendo realizar a modificação de um membro, ou demarcar que um método em específico não pode ser modificado.<br/>
Começando pelo _abstract_, essa assinatura basicamente indica que um membro da classe (no nosso caso os métodos) deve obrigatóriamente modificar esse membro caso tenha uma herança, indicando que a implementação é fornecida pelas classes derivadas, sendo assim, caso a classe derivada não implemente esse método, vai ser gerado um erro em tempo de compilação (CS0534).<br/>

```csharp
class ClasseDerivadaOmitindoMetodo : Classe
{
    // Gera erro (CS0534)
}

class ClasseDerivada : Classe
{
    protected override void MetodoAbstrato()
    {

    }
}


abstract class Classe
{
    protected abstract void MetodoAbstrato();
}
```

Os membros virtuais seguem a mesma lógica do dos abstratos, a única coisa que os diferem é a obrigatóriedade, quando utilizamos o `virtual` ao invés do `abstract` o compilador não vai gerar um erro no membro caso ele não seja sobrescrito, tornando-o opicional como pode ser visto no seguinte exemplo.

```csharp
class ClasseDerivadaOmitindoMetodo : Classe
{
    // Não gera erro
}

class ClasseDerivada : Classe
{
    protected override void MetodoAbstrato()
    {

    }
}


class Classe
{
    protected virtual void MetodoAbstrato()
    {

    }
}
```

Passando agora para os métodos selados, esse modificador é usado nos métodos para evitar que eles sejam sobrescritos, sendo assim, a palavra `sealed` sempre vai estar em conjunto com o `override` nos métodos. No caso de descumprimento do selamento, se por ventura algum método force sobrescrever um outro _sealed_, ele vai ser barrado pelo compilador, que irá gerar um erro CS0239.

```csharp
class ClasseDerivadaDaDerivada : ClasseDerivada
{
    protected override void MetodoAbstrato()
    {
        // Erro (CS0239)
    }
}

class ClasseDerivada : Classe
{
    protected sealed override void MetodoAbstrato()
    {

    }
}


class Classe
{
    protected virtual void MetodoAbstrato()
    {

    }
}
```

O método que deriva do _abstract_ ou _virtual_ deve sempre utilizar a palavra reservada `override`, para indicar ao compilador que aquele método vai sobrescrever o da classe pai, e também o nível de acessibilidade deve ser o mesmo.

Sobre métodos abstratos e virtuais é importante salientar que caso algum método utilize um dos dois, ele deve ser no mínimo protegido (_protected_), não permitindo que ele seja privado. Isso acaba fazendo sentido, por conta de que se ele fosse privado, ele só poderia ser visto no escopo da própria classe, e não de uma derivada.


#### async
#### static
  Métodos com assinatura `static` não compartilham do contexto da classe, como o próprio nome diz, eles são estáticos e não tem um 'estado'.
  
### Retornos

#### void
#### object

### Nomenclatura do método

### Parâmetros tipados e não tipados

### Utilização

#### Utilização sem retorno
#### Utilização com retorno
#### Utilização com parâmetros
#### Utilização com parâmetros tipados
  Falar sobre `System.Text.Json.JsonSerializar`
  
#### Utilização abstract e virtual
#### Utilização sealed
#### Utilização static

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
podendo ser úteis organizar o código, promover reutilização e modularidade, e facilitar a manutenção.

Referências: 
    Methods: https://learn.microsoft.com/pt-br/dotnet/csharp/programming-guide/classes-and-structs/methods
    Delegados: https://www.freecodecamp.org/news/action-and-func-delegates-in-c-sharp/

