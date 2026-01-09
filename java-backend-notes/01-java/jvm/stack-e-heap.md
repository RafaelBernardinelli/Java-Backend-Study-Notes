# Organização da Memória no Java: Stack vs Heap

## Visão Geral

A JVM (Java Virtual Machine) gerencia a memória da aplicação dividindo-a em diferentes áreas.  
As duas mais importantes para o desenvolvedor são:

- **Stack (Pilha)**
- **Heap (Monte)**

Entender como essas áreas funcionam é essencial para:
- Evitar bugs
- Melhorar performance
- Compreender erros como `StackOverflowError` e `OutOfMemoryError`
- Escrever código mais eficiente

---

## Stack (Pilha)

### O que é a Stack?

A **Stack** é a área de memória usada para armazenar:
- Execução de métodos
- Variáveis locais
- Referências para objetos no Heap

Cada **Thread** possui sua **própria Stack**.

---

### O que fica armazenado na Stack?

Dentro da Stack ficam os **Stack Frames**, um para cada método chamado.

Cada Stack Frame contém:
- Parâmetros do método
- Variáveis locais
- Referências para objetos
- Informações de controle (retorno do método)

---

### Exemplo prático

```java
public void metodoA() {
    int x = 10;
    metodoB();
}

public void metodoB() {
    int y = 20;
}
```

Durante a execução:

metodoA() é chamado → Stack Frame criado

x = 10 é armazenado na Stack

metodoB() é chamado → novo Stack Frame

y = 20 é armazenado

metodoB() termina → Stack Frame removido

metodoA() termina → Stack Frame removido

## 👉 A Stack funciona como LIFO (Last In, First Out).

## Características da Stack

Acesso muito rápido

Memória automática (não depende do Garbage Collector)

Escopo limitado ao método

Não compartilhada entre threads

Tamanho limitado

Erro comum: StackOverflowError

Ocorre quando:

Muitos métodos são empilhados

Geralmente causado por recursão infinita

public void loop() {
    loop();
}

## Heap (Monte)
O que é a Heap?

A Heap é a área de memória onde ficam:

Objetos

Arrays

Instâncias de classes

Ela é compartilhada entre todas as threads.

## O que fica armazenado na Heap?

Na Heap ficam:

Objetos criados com new

Atributos de instância

Conteúdo real dos objetos

## Exemplo prático
```java
public void exemplo() {
    Pessoa p = new Pessoa("Rafael");
}
```


## O que acontece:

p (referência) → Stack

new Pessoa("Rafael") → Heap

Stack                  Heap
-----                  -----
p  ----------------->  Pessoa { nome = "Rafael" }

## Características da Heap

Acesso mais lento que a Stack

Gerenciada pelo Garbage Collector

Compartilhada entre threads

Armazena objetos de longa duração

Tamanho configurável (-Xmx, -Xms)

Erro comum: OutOfMemoryError

Ocorre quando:

A Heap está cheia

Muitos objetos vivos

Memory leak (referências não liberadas)

List<Object> lista = new ArrayList<>();
while (true) {
    lista.add(new Object());
}

Tipos de Dados: Onde ficam?
Primitivos
int a = 10;
double b = 20.5;

Ficam diretamente na Stack (quando são variáveis locais)

Objetos
String nome = "Java";

nome (referência) → Stack

"Java" (objeto String) → Heap (String Pool)

## Stack vs Heap (Resumo)
Característica	Stack	Heap
Tipo de memória	Pilha	Monte
Armazena	Variáveis locais, referências	Objetos e arrays
Velocidade	Muito rápida	Mais lenta
Gerenciamento	Automático	Garbage Collector
Escopo	Método	Global
Compartilhamento	Por thread	Entre threads
Erros comuns	StackOverflowError	OutOfMemoryError
Garbage Collector e Heap

## O Garbage Collector (GC):

- Remove objetos da Heap que não possuem mais referências

- Nunca atua sobre a Stack

- Trabalha automaticamente

Exemplo:

Pessoa p = new Pessoa("Ana");
p = null; // objeto elegível para GC

## Dicas Importantes para o Dia a Dia

- Evite criar objetos desnecessários

- Atenção a loops que criam objetos

- Cuidado com recursões profundas

- Sempre feche recursos (streams, conexões)

- Use ferramentas como VisualVM e JConsole

## Conclusão

- Stack: rápida, pequena, controlada por métodos

- Heap: flexível, grande, gerenciada pelo GC

Entender essa divisão ajuda a escrever código mais eficiente, seguro e escalável

equals compara valores dos objetos
== compara referencia