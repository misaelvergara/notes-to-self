# Introdução

Iremos rever alguns conceitos de testes de desenvolvimento e como os aplicar no Jest.



## Testes Unitários

**Definição**: validar que partes individuais de um módulo funcionam como esperado. 

Vamos analisar o seguinte exemplo:



Ex: seja este o formato dos dados de nosso banco. Um array de usuários:

```javascript
// documentos do banco de dados
module.exports = [
  {
    name: 'João',
    lastName: 'Silva Souza',
    nickName: 'jao__123',
    password: 'password_secreta123'
  },
  {
    name: 'Pedro',
    lastName: 'Albuquerque Santos',
    nickName: 'the_pedro',
    password: 'pedro987@'
  },
  {
    name: 'Luiza',
    lastName: 'Gonçalves',
    nickName: 'lulu',
    password: 'arquitetura2019'
  }
];

```

***



Ex: seja este nosso código de produção:

```javascript
// user-loader.js
// retorna um array de usuário do banco de dados
const requestUsers = require('./request-users');

const formatUser = user => {
  const fullName = user.name + ' ' + user.lastName;
  const nickName = user.nickName;

  return { fullName, nickName };
};

const loadUsers = async () => {
  const users = await requestUsers();
  let formattedUsers = [];

  for (let user of users) {
    formattedUsers.push(formatUser(user));
  }
  return formattedUsers;
};

module.exports = {
  loadUsers,
  formatUser
};
```

***



Ex: teste unitário de user-loader.js

```javascript
// user-loader.test.js
const userLoader = require('./user-loader.js');

describe('formatUser(user)', () => {
  it("returns user's full name", () => {
    const user = {
      name: 'João',
      lastName: 'Silva Souza',
      nickName: 'jao_123',
      password: 'password_secreta123'
    }
    
    const formattedUser = userLoader.formatUser(user);

    expect(formattedUser).toEqual(
      expect.objectContaining({
        fullName: 'João Silva Souza'
      })
    );
  });
});
```

Este seria um exemplo de teste unitário que todos nós utilizamos nos testes atuais. 



**Uma dúvida**... Como seria possível testar a função **`loadUsers()`**?



## Definição: Testes de Integração

**Definição**: valida que partes individuais funcionam de forma adequada em conjunto.



Notamos que **`requestUsers()`** é uma dependência de **`loadUsers()`**, pois ela está sendo chamada no escopo da função. 

```js
// ...
const loadUsers = async () => {
  const users = await requestUsers();
// ...
```



Portanto, ao testar  **`loadUsers()`**, será necessário interceptar **`requestUsers()`** para que o teste seja efetivo e garanta integridade.

Notamos, portanto, que tal caso se trata de um **teste de integração**, pois se estivéssemos somente  testando **`loadUsers()`**, a função **`requestUsers()`** não precisaria ser chamada em nosso teste.



## Simulando Módulos e Funções

Significado de **`mock`**: simulado, imitado, falso.

Um mock é a "simulação" de um código. Utilizamos mocks para que os testes possam "simular" funções implementadas no código de produção.



### `jest.fn()`

**Funções mock** também, chamadas de **funções espiãs**,  permitem ao programador "espiar" o comportamento de uma função, como argumentos com quais a função foi chamada ou os resultados consecutivos retornado pela função.  No Jest, essas funções são definidas por **`jest.fn()`**.

Exemplo: 

```js
// Definimos que a variável mockedFunction é uma função mock.
const mockedFunction = jest.fn();
```

Ex: espiando os argumentos de uma função mock.

```js
mockedFunction('arg1', 'arg2');
/*
	mock.calls é um array pertencente à uma função mock que ...
	armazena o valor dos argumentos de cada chamada à função.
*/
const calls_1 = mockedFunction.mock.calls[0];
console.log(calls_1);
// -> ['arg1', 'arg2']

mockedFunction('oi', 'tdbem');
mockedFunction('teste', 3);

const calls_3 = mockedFunction.mock.calls[2];
console.log(calls_3);
// -> ['teste', 3]
```

****

Ex: espiando os resultados consecutivos de uma função mock.

```js
console.log(mockedFunction('oi'));
// -> undefined
```

Se executarmos uma função mock **sem implementá-la** (implementar um método ou uma função significa definir um corpo para ele), ela irá retornar, por padrão, o valor **`undefined`**.

Para espiar o resultado de uma função mock, é necessário que esta nos retorne algum resultado. Para isso, o Jest nos possibilita **duas formas de atribuir um resultado à uma função mock**.

1. Definindo valores de retorno indiscretamente;
2. Implementando o corpo da função.



#### Definindo valores de retorno indiscretamente para uma função mock

1. **`mockReturnValueOnce()`**

```js
mockedFunction.mockReturnValueOnce('string de texto');

mockedFunction();
// -> 'string de texto'
mockedFunction();
// -> undefined

mockedFunction.mockReturnValueOnce('string de texto');
mockedFunction.mockReturnValueOnce(123);
mockedFunction.mockReturnValueOnce('oi');

mockedFunction();
// -> 'string de texto'
mockedFunction();
// -> 123
mockedFunction();
// -> 'oi'
mockedFunction();
// -> undefined
```

2. **`mockReturnValue()`**

```js
mockedFunction.mockReturnValue('sempre');

mockReturnValue();
// -> 'sempre'
mockReturnValue();
// -> 'sempre'
// ...

const newMockedFn = jest.fn();
newMockedFn.mockReturnOnce('primeira chamada');
newMockedFn.mockReturnOnce('segunda chamada');
newMockedFn.mockReturnValue('após');

newMockedFn();
// -> 'primeira chamada'
newMockedFn();
// -> 'segunda chamada'
newMockedFn();
// -> 'após'
newMockedFn();
// -> 'após'
// ...
```



#### Implementando o corpo de uma função mock

Existem duas formas intercambiáveis de se implementar uma função mock.

1. Definindo a implementação da função como argumento de **`jest.fn()`**.

```js
const mockFn = jest.fn((arg, arg2) => {
    const newArg = arg + arg2;
    
    console.log(`old "${arg}"`);
    console.log(`new "${newArg}"`)
    
    return newArg;
});

const result = mockFn('oi', 'td bem?');
// -> old "oi"
// -> new "oitdbem?"

console.log(result);
// -> 'oitdbem?'
```



2. Utilizando a propriedade **`mockImplementation`**.

```js
   mockFn.mockImplementation((arg) => {
       console.log('oi');
       return arg;
   });
```

   		

#### Acessando os resultados de uma função mock

```js
const myMock = jest.fn(res => {
    if (!res) throw new Error('Um argumento deve ser especificado.');
	return `res: ${res}`
});

myMock('oi');
myMock([{ token: 'não leia! esse token é secreto' }]);
myMock();

console.log(myMock.mock.results);
/* -> 
[
  	{
    	type: 'return',
    	value: 'oi',
    },
  	{
    	type: 'return',
    	value: [
    		{ 
    			token: 'não leia! esse token é secreto' 
    		}
    	]
  	},
  	{
    	type: 'throw',
    	value: 'Um argumento deve ser especificado.',
  	},
];
*/
```



### `jest.mock()`

Anteriormente, vimos que seria necessário interceptar a função **`requestUsers()`** para que o teste de **`loadUsers()`** seja realizado de forma adequada. Certo, nosso alvo é o módulo `./user-loader` e notamos que este módulo importa a função **`requestUsers()`** de outro módulo. Agora, vamos ver, brevemente, o que o Jest tem a oferecer para executarmos essa tarefa com o **`jest.mock()`**.



#### Para que serve?

A função **`jest.mock()`** cria uma versão simulada de um módulo. Assim, o módulo real não será executado, mas, sim, uma versão simulada deste.



#### Utilizando a função `jest.mock()`

A função recebe, por padrão, **o caminho de um módulo** como primeiro argumento. Assim que o caminho for especificado e a função chamada, o módulo será simulado automaticamente pelo Jest.



Ex: arquivo que queremos testar.

```js
// index.js
const requestUsers = require('./request-users');

const logUsers = async () => {
    const users = await requestUsers();
    console.log(users);
}

module.exports = logUsers;
```



Ex: arquivo de teste.

```js
//index.test.js
jest.mock('./request-users');

const logUsers = require('./index');

it('calls requestUsers', () => {
	logUsers();
    // -> undefined
});
```



Ao executarmos a função **`logUsers()`**, é mostrado no terminal uma linha de **`console.log(users)`** printando `undefined`. Por quê?

```js
// ...
const logUsers = async () => {
    const users = await requestUsers();
    console.log(users);
}
// ...
```



Bem, quando definimos que iremos simular o módulo `./request-users` com a declaração de `jest.mock('./request-users')`, o Jest sobrescreve a função exportada pelo módulo com **uma função mock**. Ou seja, quando **`requestUsers()`** é chamado por **`logUsers()`**, uma função mock será executada **ao invés da função real**. E, portanto, quando printamos `users`, recebemos, na verdade, o retorno de uma função mock, que é `undefined`.



**Por que foi retornado `undefined`?**

Pois, o Jest simulou o módulo `./request-users` automaticamente. Quando o Jest simula um módulo, ele atribui uma função mock para cada variável que o módulo exporta. Quando o Jest atribui essas funções mock automaticamente, ele não as implementa (não define um corpo para as funções). E, como vimos anteriormente, **funções mock não implementadas** retornam `undefined`.

Sendo assim, resta uma questão: como implementar as funções mock de um módulo simulado?



#### Implementando funções mock de um módulo simulado

1. Será necessário importar o módulo simulado **dentro do arquivo de teste**.

```js
//index.test.js
jest.mock('./request-users');
const requestUsers = require('./request-users');
```

2. Implementar a função mock com **`mockImplementation`**. Como o módulo `./request-users` retorna somente a função **`requestUsers()`**, iremos somente implementar uma função.

```js
requestUsers.mockImplementation(() => {
    console.log('implementação');
    return [{ user: 'Matheus' }, { user: 'Gustavo' }]
});
```

Pronto '-'



Agora, ao executarmos o teste, **`logUsers()`** irá printar o array `[{ user: 'Matheus' }, { user: 'Gustavo' }]`:
```js
// index.js
const requestUsers = require('./request-users');

const logUsers = async () => {
    const users = await requestUsers();
    console.log(users);
}

module.exports = logUsers;

//index.test.js
jest.mock('./request-users');
const requestUsers = require('./request-users');

requestUsers.mockImplementation(() => {
    console.log('implementação');
    return [{ user: 'Matheus' }, { user: 'Gustavo' }]
});

const logUsers = require('./index');

it('calls requestUsers', () => {
	logUsers();
    // -> [{ user: 'Matheus' }, { user: 'Gustavo' }]
});
```



Voltando ao primeiro caso:

```js
// user-loader.js
const requestUsers = require('./request-users');

const formatUser = user => {
  const fullName = user.name + ' ' + user.lastName;
  const nickName = user.nickName;

  return { fullName, nickName };
};

const loadUsers = async () => {
  const users = await requestUsers();
  let formattedUsers = [];

  for (let user of users) {
    formattedUsers.push(formatUser(user));
  }
  return formattedUsers;
};

module.exports = {
  loadUsers,
  formatUser
};

// user-loader.test.js
const userLoader = require('./user-loader.js');

const requestUsers = require('./request-users');
jest.mock('./request-users');

requestUsers.mockImplementation(() => {
  console.log('Simulando uma requisição...');
  return [
    {
      name: 'João',
      lastName: 'Silva Souza',
      nickName: 'jao_123',
      password: 'password_secreta123'
    },
    {
      name: 'Maria',
      lastName: 'José',
      nickName: 'mariazinha',
      password: 'maria2'
    }
  ];
});

it('loadUsers()', async () => {
  const loadedUsers = await userLoader.loadUsers();
  expect(requestUsers).toBeCalled();

  expect(loadedUsers[0]).toEqual({
    fullName: 'João Silva Souza',
    nickName: 'jao_123'
  });
});
```



#### Simulando módulos que exportam mais de uma variável (named exports)

Ex: seja o módulo greet-methods.js:

```js
// greet-methods.js
const helloWorld = () => {
  console.log('olá world');
};

const greet = name => {
  console.log(`oi, ${name}`);
};

const farewell = name => {
  console.log(`tchau, ${name}`);
};

module.exports = {
  farewell,
  greet,
  helloWorld
};
```



 O módulo acima não apresenta um caso real em que iremos precisar simular as variáveis de um módulo. No entanto, iremos supor o seguinte cenário: preciso criar uma simulação da função **`greet()`**, mas, quero **manter as implementações originais** das outras funções deste módulo.



Iremos começar criando um mock do módulo `./greet-methods.js` e analisando as funções obtidas após o processo de simulação.

```js
jest.mock('./greet-methods.js');
const greetMethods = require('./greet-methods');

console.log(greetMethods);
/*
     {
        farewell: [Function: farewell] {
          _isMockFunction: true,
          ...
        },
        greet: [Function: greet] {
        _isMockFunction: true,
          ...
        },
          helloWorld: [Function: helloWorld] {
          _isMockFunction: true,
          ...
        }
      }
*/
```

Certo. Notamos que todas as funções do módulo `./greet-methods.js` foram substituídas por **funções mock**, uma vez que declaramos que o módulo será simulado via `jest.mock()`.



Agora, queremos implementar o corpo da função mock para a função **`greet()`**. Poderíamos simplesmente fazer o seguinte:

```js
jest.mock('./greet-methods.js');
const greetMethods = require('./greet-methods');

greetMethods.greet.mockImplementation(() => {
  console.log('hello mundo');
});

it('tests greet()', () => {
  greetMethods.greet();
    // -> hello mundo
});

```



No entanto, ao executar as outras funções do módulo importado, notamos que elas simplesmente perdem a implementação original. Isso acontece porque agora elas são funções mock.

```js
// ...
  greetMethods.greet();
    // -> hello mundo
  greetMethods.helloWorld();
    //
  greetMethods.farewell();
    //
// ...
```



Como queremos **somente** simular a função **`greet()`**, podemos utilizar de dois artifícios do Jest: **`jest.requireActual()`** e o segundo argumento opcional de `jest.mock()`:

- **`jest.mock('./module_path', ?factory)`**

```js
const mockGreetMethods = () => {
  const actualGreetMethods = jest.requireActual('./greet-methods.js');
  return {
    ...actualGreetMethods,
    greet: jest.fn(() => {
      console.log('hello mundo');
    })
  };
};

jest.mock('./greet-methods.js', () => mockGreetMethods());
const greetMethods = require('./greet-methods');

it('tests greet()', () => {
  greetMethods.greet();
    // -> hello mundo
  greetMethods.helloWorld();
    // -> olá world
  greetMethods.farewell();
    // tchau, undefined
});

```

Agora, notamos que as funções mantiveram as implementações originais, mas, a função **`greet()`** foi **substituída por uma função mock**.



Explicando a sintaxe:

**`mockGreetMethods()`** - é uma função que retorna um objeto. Este objeto corresponde às variáveis exportadas pelo módulo  `./greet-methods.js`. 

**`jest.requireActual()`** - importa as funções **reais** do módulo. Recebemos elas como um objeto contento as variáveis exportadas pelo módulo.



**`jest.mock('./greet-methods.js', () => mockGreetMethods());`** - o segundo argumento determina uma **factory**, que é uma função que irá substituir a implementação do nosso módulo. O Jest aceita **somente funções de linha** como um argumento para a factory.  Exemplo de função de linha:

```js
const inlineFunction = () => {
    console.log('oi');
}
```



Sendo assim, declaramos uma função de linha que executa a função `mockGreetMethods()`, esta que, por sua vez, retorna um objeto ao ser executada. Estamos, portanto, retornando um objeto quando a função de linha for executada.



### Pegadinhas do Jest

O Jest utiliza o Babel para poder executar a aplicação em modo de teste. Por isso, algumas normas foram estabelecidas para garantir o funcionamento deste mecanismo.

#### Hoisting

É uma técnica que é executada em tempo de execução. **To hoist** significa **levantar**, e é justamente o que acontece com certas partes de nosso código ao executá-lo. Certas partes "levantam", vão para o topo do arquivo, para que possam ser executados primeiro. Exemplo no jest:

Ex: como declaramos no arquivo.

```js
// user-loader.test.js
const userLoader = require('./user-loader.js');

const requestUsers = require('./request-users');
jest.mock('./request-users');

requestUsers.mockImplementation(() => {
  // ...
});

```

Como o Babel compila:

```js
jest.mock('./request-users');
requestUsers.mockImplementation(() => {
  // ...
});
const requestUsers = require('./request-users');
const userLoader = require('./user-loader.js');
```



Outro exemplo:

```js
jest.mock('./greet-methods.js', () => mockGreetMethods());

const greetMethods = require('./greet-methods');

const mockGreetMethods = () => {
  const actualGreetMethods = jest.requireActual('./greet-methods.js');
  return {
    ...actualGreetMethods,
    greet: jest.fn(() => {
      console.log('hello mundo');
    })
  };
};
// ....
```



O que será executado pelo Jest:

```js
const mockGreetMethods = () => {
  const actualGreetMethods = jest.requireActual('./greet-methods.js');
  return {
    ...actualGreetMethods,
    greet: jest.fn(() => {
      console.log('hello mundo');
    })
  };
};
jest.mock('./greet-methods.js', () => mockGreetMethods());

const greetMethods = require('./greet-methods');
// ....
```

Note que a função **`mockGreetMethods()`** foi para o topo do arquivo. Isso acontece porque a declaramos com a palavra "mock" antes dela, e, portanto, o Babel interpreta que esta função deve ser elevada. 



Se tivéssemos definido-a com outro nome, ela seria tratada como uma variável comum, e o Jest iria lançar uma exceção, pois não teria acesso à função - uma vez que ela foi declarada somente após `jest.mock()` ser executado.

```js
jest.mock('./greet-methods.js', () => newGreetMethods());

const newGreetMethods = () => {
  const actualGreetMethods = jest.requireActual('./greet-methods.js');
  return {
    ...actualGreetMethods,
    greet: jest.fn(() => {
      console.log('hello mundo');
    })
  };
};

const greetMethods = require('./greet-methods');
// ....
```





Referências:


> https://www.sitepoint.com/javascript-testing-unit-functional-integration/ 

> https://jestjs.io/docs/en/mock-functions