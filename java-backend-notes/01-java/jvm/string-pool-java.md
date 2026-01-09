## String Pool no Java

### O que é o String Pool?

O **String Pool** é uma área especial da **Heap** usada pela JVM para armazenar **Strings imutáveis** reutilizáveis.

Seu objetivo é:
- Economizar memória
- Evitar criação desnecessária de objetos `String`
- Melhorar performance em comparações

👉 O String Pool faz parte da Heap, **não da Stack**.

---

### String é um objeto especial

Apesar de `String` ser um objeto como qualquer outro:
- É **imutável**
- Possui um **pool dedicado**
- Pode ser reutilizada automaticamente pela JVM

---

## Criação de Strings: literal vs new

### String criada como literal

```java
String s1 = "Java";
String s2 = "Java";


O que acontece:

A JVM verifica se "Java" já existe no String Pool

Se existir → reutiliza o mesmo objeto

Se não existir → cria e adiciona ao Pool

Resultado:

s1 ---> "Java" <--- s2

System.out.println(s1 == s2); // true


👉 Ambos apontam para o mesmo objeto na Heap (String Pool).

String criada com new
String s3 = new String("Java");


O que acontece:

"Java" literal vai para o String Pool (se ainda não existir)

new String("Java") cria um novo objeto fora do Pool

String Pool          Heap (fora do Pool)
-----------          -------------------
"Java"        <--    new String("Java")

System.out.println(s1 == s3); // false
System.out.println(s1.equals(s3)); // true


👉 Conteúdo igual, referências diferentes.

Comparação: == vs equals
Usando ==

Compara referência de memória

Indica se apontam para o mesmo objeto

String a = "Teste";
String b = "Teste";

a == b // true

Usando equals()

Compara conteúdo

Deve ser usado sempre para Strings

String a = new String("Teste");
String b = new String("Teste");

a.equals(b) // true
a == b      // false

Método intern()
O que faz o intern()?

O método intern():

Força uma String a entrar no String Pool

Retorna a referência do Pool

String s1 = new String("Java");
String s2 = s1.intern();
String s3 = "Java";

s2 == s3 // true

Quando usar intern?

⚠️ Use com cuidado

Pode reduzir memória em cenários específicos

Pode causar pressão no Pool se usado excessivamente

Raramente necessário em aplicações modernas

String Pool e Garbage Collector

Strings no Pool podem ser coletadas pelo GC

Desde o Java 7, o Pool fica na Heap (antes ficava na PermGen)

String s = "Temp";
s = null; // String elegível para GC


👉 Se nenhuma referência existir, o GC pode limpar.

Strings, Imutabilidade e Performance
String s = "Java";
s.concat(" Spring");


❌ Isso NÃO altera a String original.

✔ Um novo objeto é criado.

Por isso, em loops ou concatenações frequentes, use:

StringBuilder sb = new StringBuilder();
sb.append("Java");
sb.append(" Spring");

Boas práticas com String Pool

Prefira literais quando possível

Nunca use == para comparar conteúdo

Evite new String("texto") sem necessidade

Use StringBuilder ou StringBuffer para concatenação

Entenda o impacto em memória em sistemas de alto volume

Resumo rápido
Situação	Vai para o Pool?
"Java"	✅ Sim
new String("Java")	❌ Não
intern()	✅ Força entrada
Comparação com ==	⚠️ Referência
Comparação com equals()	✅ Conteúdo