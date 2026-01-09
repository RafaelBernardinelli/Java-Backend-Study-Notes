# StringBuilder e StringBuffer no Java

## Contexto: por que eles existem?

Em Java, `String` é **imutável**.  
Isso significa que **qualquer modificação cria um novo objeto na Heap**.

```java
String s = "Java";
s = s + " Spring";

O que acontece internamente:

"Java" → Heap

" Spring" → Heap

"Java Spring" → novo objeto na Heap

❌ Em loops, isso causa:

Alto consumo de memória

Pressão no Garbage Collector

Perda de performance

Para resolver isso, surgem:

StringBuilder

StringBuffer

O que é StringBuilder?

StringBuilder é uma classe mutável usada para manipulação eficiente de Strings.

Características principais

Mutável

Não é thread-safe

Mais rápido

Usa um buffer interno de caracteres

Ideal para uso em single-thread

StringBuilder sb = new StringBuilder();
sb.append("Java");
sb.append(" Spring");


👉 O mesmo objeto é reutilizado, sem criar novas Strings.

O que é StringBuffer?

StringBuffer é muito semelhante ao StringBuilder, porém:

Características principais

Mutável

Thread-safe

Métodos sincronizados

Mais lento que StringBuilder

Criado antes do Java 5

StringBuffer sb = new StringBuffer();
sb.append("Java");
sb.append(" Spring");


👉 Segurança em ambientes concorrentes, com custo de performance.

Onde ficam na memória?

A referência (sb) → Stack

O objeto StringBuilder / StringBuffer → Heap

O buffer interno (char[]) → Heap

Nenhuma interação direta com o String Pool.

Comparação: String vs StringBuilder vs StringBuffer
Característica	String	StringBuilder	StringBuffer
Mutável	❌ Não	✅ Sim	✅ Sim
Thread-safe	✅ Sim (imutável)	❌ Não	✅ Sim
Performance	❌ Baixa em concatenação	✅ Alta	⚠️ Média
Uso em loop	❌ Não recomendado	✅ Recomendado	⚠️ Só se precisar
Sincronização	Não precisa	Não tem	synchronized
Exemplo prático: loop
❌ Usando String (ruim)
String s = "";
for (int i = 0; i < 1000; i++) {
    s += i;
}


Cria milhares de objetos

Impacta GC

Código ineficiente

✅ Usando StringBuilder (correto)
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);
}
String resultado = sb.toString();


Um único objeto

Muito mais rápido

Menor consumo de memória

StringBuffer é realmente necessário?

Hoje, quase nunca.

Motivos:

StringBuilder + controle de concorrência externo é melhor

StringBuffer sincroniza tudo (overhead desnecessário)

Concorrência fina é melhor resolvida com:

synchronized

Lock

Thread confinement

Quando usar cada um?
Use String quando:

Texto é fixo ou pouco modificado

Leitura frequente

Compartilhamento seguro entre threads

Use StringBuilder quando:

Concatenação frequente

Loops

Código single-thread

Construção de JSON, logs, mensagens

Use StringBuffer quando:

Código legado

APIs antigas exigem

Concorrência simples e inevitável

Dica de performance: capacidade inicial

Evite realocação de buffer:

StringBuilder sb = new StringBuilder(1024);


👉 Menos cópias de array → melhor performance.

Internamente: como funciona?

Ambos usam um char[] interno

Ao exceder a capacidade:

Um novo array maior é criado

Conteúdo é copiado

StringBuilder não sincroniza

StringBuffer sincroniza todos os métodos

Armadilha comum
StringBuilder sb = new StringBuilder("Java");
String s = sb.toString();
sb.append(" Spring");


❗ s NÃO muda, pois toString() cria uma nova String.

Conclusão

String é simples e segura, mas imutável

StringBuilder é a melhor escolha na maioria dos casos

StringBuffer existe por compatibilidade e casos específicos

Saber escolher evita problemas de performance e concorrência

Resumo mental rápido

String = imutável
StringBuilder = rápido
StringBuffer = seguro, porém lento