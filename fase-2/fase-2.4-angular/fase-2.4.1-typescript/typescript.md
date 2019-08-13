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
Uma cadeia de carácteres modelo, declaradas usando `\``, podem ser usadas para formatar uma cadeia
de carácteres usando código TypeScript.

```typeScript
let firstName: string = "Roberta";
let lastName: string = "Árvore";
let age: number = 19;

let info: string = `${firstName} ${lastName} ${age + 1}!!` //Roberta Árvore 20!!
```
