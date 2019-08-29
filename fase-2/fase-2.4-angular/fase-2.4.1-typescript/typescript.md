# Fase 2.4.1 - TypeScript

## Introdução
TypeScript possui os mesmos tipos de JavaScript (Boolean, Number, String, Objeto, etc.), e podemos
determinar os tipos de uma variável fortmente.

### Boolean
Boleanos são o tipo mais simples, podendo assumir somente dois valores `true` ou `false`. No
TypeScript temos a palavra reservada `boolean`.

```typescript
let estaFeito: boolean = false;
```

### Number
Em TypeScript, todos os números são declarados com a palavra reservada `number`, e assim como em
JavaScript, todos os números são valores de ponto flutuante. TS também suporta declarações
de hexadecimais, binários e octadecimais.

```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binario: number = 0b1010;
let octa: number = 0o744;
```

### String
Uma cadeia de caractéres é declarada usando a palavra reservada `string`, há duas maneiras
de criar strings, usando `"` ou `'`.

```typescript
let cor: string = "vermelho";
cor = 'azul';
```

#### Template Strings
Uma cadeia de carácteres modelo, declaradas usando ``` (crase), podem ser usadas para formatar uma
cadeia de carácteres usando código TypeScript.

```typeScript
let primeiroNome: string = "Roberta";
let ultimoNome: string = "Árvore";
let idade: number = 19;

let info: string = `${primeiroNome} ${ultimoNome} ${idade + 1}!!` //Roberta Árvore 20!!
```

### Array
Listas são declaradas colocando `[]` na frente de um dos outros tipos.

```typescript
let listaNumeros: number[] = [1, 2, 3];
let listaPalavras: string[] = ["Foo", "Barr"];
``` 

### Enum
Enumerações são um jeito fácil de declarar um conjunto de variáveis com valores constantes, e são
criados usando a palavra chave `enum` antes do nome da enumeração. No geral, enumerações
usam valores em sequência, iniciando do `0`.

```typescript
enum Cor {
  Vermelho, // = 0
  Azul, // = 1
  Verde, // = 2
}
```

Você também pode usar valores inseridos manualmente, em um ou todos os membros da enumeração. Em
particular, mudar o valor de uma das chaves da enumeração, muda o inicio da sequência para as
próximas chaves.

```typescript
enum Cor {
  Vermelho = 3, // = 3
  Azul, // = 4
  Verde = 7, // = 7
  Amarelo, // = 8
}
```

### Object
Variáveis do tipo `object` aceitam grupos de pares chave-valor, similares aos JSONs do JavaScript.
Iremos aprofundar em objetos ao falarmos de classes e interfaces.

```typescript
let obj: object = {
  primeiroNome: "Roberta",
  ultimoNome: "Árvore",
}
```

### Any
Esse tipo pode equivaler a qualquer outro tipo do TypeScript, uma variável que usa o tipo `any` pode
ter qualquer tipo de valor.

```typescript
let x: any = 4
x = "pode ser uma palavra"
x = false
```

**Observação**: evite usar `any` o máximo possível, usando esse tipo, a maior vantidadem de usar 
TypeScript, a tipidadem forte, não terá efeito.

### Outros tipos
Tipos como `void`, `null` e `undefined` são utéis somente para declarações de funções, e serão
aprofundados mais tarde, quando falarmos sobre funções.

## Declaração de variáveis
Em TypeScript, há três formas de declarar variáveis, usando `var`, `let` e `const`.

### var
A palavra `var` nos permite declarar variáveis que mudam tanto de valor, quanto de escopo, e
também podem ser redeclaradas.

```typescript
if (true) {
  var x: number = 4;
  var y: number = 5;
}

var y: string = "Foo";
console.log(x); // imprime 4
console.log(y); // imprime Foo
```

Como a variável `x` foi declarada usando `var` ela é acessível fora do escopo do `if`. Isto
combinada ao fato de que variáveis `var` podem ser redeclaradas, podem ocorrer erros onde
sobrescrevemos variáveis declaradas em bibliotecas que importamos sem perceber, gerando erros
incrivelmente difíceis de encontrar.

Via de regra, evite usar `var`.

## let
A palavra `let` nos permite declarar variáveis que mudam somente de valor, elas mantêem seu escopo
e não podem ser redeclaradas

```typescript
let x: number = 4;
x = 5;

console.log(x) // 4
```

```typescript
let x: number = 4;
let x: number = 5; // compilador irá jogar um erro
```

```typescript
if (true) {
  let x: number = 4;
}

console.log(x); // compilador irá jogar um erro
```

## const 
A palavra `const` nos permite declarar variáveis que não mudam de valor, escopo e não podem
ser redeclaradas. E um valor só pode ser associado a uma variável deste tipo em sua declaração

```typescript
const x: number = 5; 

console.log(x) // 5
```

```typescript
const x: number = 4;
x = 5; // compilador irá jogar um erro

console.log(x) // 4
```

```typescript
const x: number; // compilador irá jogar um erro
```

```typescript
const x: number = 4;
const x: number = 5; // compilador irá jogar um erro
```

```typescript
if (true) {
  const x: number = 4;
}

console.log(x); // compilador irá jogar um erro
```

## Interfaces

Quando declaramos uma variável com o tipo `object` não determinamos o formato do objeto, ou seja,
ele pode ter qualquer chave, com qualquer valor. Se usarmos `interfaces`, podemos garantir
que um objeto tenho certas chaves e quais os tipos dos valores para cada chave.

```typescript
interface FullName {
  primeiroNome: string;
  ultimoNome: string;
}

const obj: FullName = {
  primeiroNome: "Roberta",
  ultimoNome: "Árvore",
}
```

Se `obj` não tiver `primeiroNome` ou `ultimoNome` presentes ou o valor associado a essas chaves não
for do tipo `string` o compilador irá jogar um erro.

### Valores opcionais

Se quisermos indicar que alguma das propriedades não é obrigatória, podemos colocar `?` logo
depois do nome da propriedade.

```typescript
interface FullName {
  primeiroNome: string;
  segundoNome?: string;
  ultimoNome: string;
}

const name1: FullName = {
  primeiroNome: "Roberta",
  ultimoNome: "Árvore",
}

const name2: FullName = {
  primeiroNome: "Lucas",
  segundoNome: "Santos",
  ultimoNome: "Silva",
}
```

### Propriedades de somente leitura
Se quisermos que uma das propriedades não sejam mudadas após a declaração do objeto, podemos a
palavra `readonly`.

```typescript
interface Ponto {
  readonly x: number;
  readonly y: number;
}

const ponto: Ponto = { x: 10, y: 10 };
ponto.x = 20 // compilador irá jogar um erro
```

### Interface extensíveis
Se quisermos que além das propriedades declaradas, a interface possa aceitar chaves além das
declaradas podemos declarar tipos indexaveis dentro dela.

```typescript
interface Ponto {
  readonly x: number;
  readonly y: number;
  [key: string]: number;
}
```

Agora a interface `Ponto` além de `x` e `y`, ela aceita qualquer par em que a chave seja uma 
`string` e o valor seja um `número`.


### Herança de interfaces

Podemos criar uma interface que herda todas as propriedades de outra interface, usando a palavra
`extends`.

```typescript
interface Ponto {
  x: number;
  y: number;
}

interface Ponto3D extends Ponto {
  z: number;
}

const ponto3d: Ponto3D = {
  x: 10,
  y: 10,
  z: 15,
};
```

Como `Ponto3D` extende `Ponto`, `Ponto3D` recebe tudo que foi declarado em `Ponto`.

## Funções

Funções são blocos de código que podem ser re-executados, aumentando a reusabilidade do código. E
podem ser declaradas usando a palavra `function`. Podemos tipar os argumentos da função,
e o tipo que essa função retorna, usamos o tipo `void`, caso a função não retorne nada.

```typescript
function somaUm(x: number): number {
  return x + 1;
}

function imprime(palavra: string): void {
  console.log(palavra);
}

somaUm(4) // retorna 5
imprime("Foo") // não retorna nada
```