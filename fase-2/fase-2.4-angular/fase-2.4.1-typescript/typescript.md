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
let firstName: string = "Roberta";
let lastName: string = "Árvore";
let age: number = 19;

let info: string = `${firstName} ${lastName} ${age + 1}!!` //Roberta Árvore 20!!
```

### Array
Listas são declaradas colocando `[]` na frente de um dos outros tipos.

```typescript
let numberArray: number[] = [1, 2, 3];
let stringArray: string[] = ["Foo", "Barr"];
``` 

### Enum
Enumerações são um jeito fácil de declarar um conjunto de variáveis com valores constantes, e são
criados usando a palavra chave `enum` antes do nome da enumeração. No geral, enumerações
usam valores em sequência, iniciando do `0`.

```typescript
enum Color {
  Red, // = 0
  Blue, // = 1
  Green, // = 2
}
```

Você também pode usar valores inseridos manualmente, em um ou todos os membros da enumeração. Em
particular, mudar o valor de uma das chaves da enumeração, muda o inicio da sequência para as
próximas chaves.

```typescript
enum Color {
  Red = 3, // = 3
  Blue, // = 4
  Green = 7, // = 7
  Yellow, // = 8
}
```

### Object
Variáveis do tipo `object` aceitam grupos de pares chave-valor, similares aos JSONs do JavaScript.
Iremos aprofundar em objetos ao falarmos de classes e interfaces.

```typescript
let obj: object = {
  firstName: "Roberta",
  lastName: "Árvore",
}
```

### Any
Esse tipo pode equivaler a qualquer outro tipo do TypeScript, uma variável que usa o tipo `any` pode
ter qualquer tipo de valor.

```typescript
let x: any = 4
x = "it can be a string"
x = false
```

**Observação**: evite usar `any` o máximo possível, usando esse tipo, a maior vantagem de usar 
TypeScript, a tipagem forte, não terá efeito.

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