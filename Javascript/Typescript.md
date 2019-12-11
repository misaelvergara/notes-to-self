# Introdução

O TypeScript é uma linguagem de programação que providencia **tipagem** (inferência de tipos) ao JavaScript. Em tempo de execução, a linguagem é transformada em JavaScript. Ou seja, todo e qualquer código em TypeScript é transformado (transpilado) em JavaScript na hora de ser executado. 



## Quais as vantagens de se utilizar o TypeScript ao invés do JavaScript?

Um dos benefícios do TypeScript é a aprimoração de funções fornecidas pelo IDE, como dicas (hints) e completação de código. Isso é possível porque a tipagem determina os **tipos** e **interfaces** que um código implementa. Com eles, o IDE reconhece as melhores sugestões à serem exibidas. 

Além do mais, ao se implementar tipagem em funções e variáveis, a interpretação e leitura do código passa a ser mais declarativo e legível, garantindo, também, que as variáveis tenham tipos bem definidos, evitando erros de compilação.



# Tipos Comuns

Os tipos de uma variável são declarados logo após a declaração do nome da variável. 

```typescript
// let nomeDaVariavel: tipo;
let isRaining: boolean;

isRaining = true;
isRaining = false;
isRaining = 'não'; // throws TypeError
// não é possível atribuir um valor string à uma variável do tipo boolean

// let nomeDaVariavel: tipo = valorDaVariavel;
let isCloudy: boolean = true;
```

 

Existem tipos que são bem explícitos, como por exemplo o tipo `boolean`. Seu valor só pode ser `true` ou `false`. O mesmo se aplica para outros tipo explícitos, como `string` e `number`.

```typescript
// define uma variável de nome n, que recebe o tipo number e possui o valor 12
let n: number = 12; 
n = 0123;
n = '1'; // throws TypeError
```

Além dos tipos citados, no TypeScript, `undefined` e `null` também são tipos. 

```typescript
// define uma variável de nome u, que recebe o tipo undefined e possui o valor undefined
let u: undefined = undefined;
let n: null = null;
```



No entanto, tipos como `Array` e objetos são definidos de uma forma um pouco mais específica.

```typescript
// names é o nome da variável, string[] é o tipo da variável, que define um array de strings
let names: string[] = ['joão', 'jonas', 'joana', 'jonathan'];

// Array<string> também define um array de strings
let places: Array<string> = ['Londrina', 'Londres', 'Cambé', 'Campinas'];
```

Como visto acima, ambas as formas são intercambiáveis.



Funções também recebem tipos em seu argumentos e em seu valor de retorno. Podemos definir como: 

```typescript
// define uma função de nome greetUser que recebe um argumento name do tipo string e retorna um valor do tipo string
function greetUser(name: string): string {
    return `Hello, ${name}!`;
}

greetUser('Joao'); // -> Hello, Joao!
greetUser(); // throws NotEnoughArguments
greetUser(12); // throws TypeError
```



## Definindo Interfaces

Interfaces são como modelos de objetos. É a estrutura que um objeto que implementa uma `interface` deve respeitar. São aplicadas tanto para objetos, como para classes.

```typescript
interface UserModel {
    name: string;
    address: string;
    age: number;
    // oxenti, que isso? '?:'
    description?: string;
}

const userJoao: UserModel {
    name: 'Joao',
    address: 'Rua Porto',
	age: 32,
}

function printUser(user: UserModel) {
    console.log(`${user.name}, ${user.age} anos. Localize em: ${user.address}.`);
    if (user.description) console.log(user.description);
}
    
printUser(userJoao); // ok
printUser({
    name: 'Maria',
    age: 25
}); // throws MissingArguments
```



## Declarando Tipos de Funções

```typescript
let log: (msg: string) => void;

log = (msg: string) => {
    console.log(msg);
}
```



**Parâmetros Padrões:**

```typescript
function prepare(a = '') {
    // o arg padrão infere que o tipo a ser esperado sempre é string
}
```

