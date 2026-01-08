# Parallel Streams (Java)

## 💡 O que é
`parallelStream()` é uma forma de executar operações de `Stream`
em **paralelo**, usando automaticamente múltiplos núcleos da CPU.

Internamente ele utiliza:
- `ForkJoinPool.commonPool()`

Ou seja:
> Parallel Stream = Stream + Fork/Join

---

## 🎯 Quando usar
- Processamento **CPU-bound**
- Operações puras (sem efeitos colaterais)
- Grandes volumes de dados
- Cálculos independentes entre elementos

**Exemplos reais:**
- Processar listas grandes
- Cálculo de estatísticas
- Transformações matemáticas
- Filtros complexos

---

## ❌ Quando NÃO usar
- Operações **I/O-bound**
- Chamadas HTTP
- Acesso a banco
- Escrita em arquivo
- Código com `synchronized`
- Código com estado compartilhado mutável

---

## 🧠 Relação com CPU-bound vs I/O-bound
- ✔️ Ideal para **CPU-bound**
- ❌ Péssimo para **I/O-bound**

> Parallel Streams **bloqueiam threads do ForkJoinPool**  
> Se uma thread bloquear esperando I/O → performance despenca

---

## 🧠 Relação com SOLID / Design
- **SRP:** cada função do pipeline faz uma coisa
- **OCP:** adiciona operações sem alterar o fluxo
- **Imutabilidade:** fundamental para segurança

---

## 🧵 Como funciona internamente
- Divide a coleção em partes
- Executa tarefas em paralelo
- Junta o resultado

Tudo isso é transparente para você.

---

## 🧪 Exemplo simples
```java
List<Integer> numbers = List.of(1, 2, 3, 4, 5);

int sum = numbers
    .parallelStream()
    .map(n -> n * 2)
    .sum();
🧪 Exemplo CPU-bound real

long count = users
    .parallelStream()
    .filter(u -> expensiveCalculation(u))
    .count();
🚨 Ordem de execução
Parallel Stream não garante ordem, a menos que você force:


stream()
    .parallel()
    .forEachOrdered(System.out::println);
⚠️ Forçar ordem reduz performance.

⚠️ Efeitos colaterais (perigo)

❌ Errado:
int total = 0;
list.parallelStream().forEach(n -> total += n);

✔️ Correto:
int total = list.parallelStream().mapToInt(Integer::intValue).sum();
```

## 🧵 Controle de threads

Você não controla o Executor

Usa sempre o ForkJoinPool.commonPool()

## ❌ Se precisar controlar threads → não use Parallel Stream

## 🆚 Parallel Stream vs Stream normal
Stream	Parallel Stream
Sequencial	Paralelo
Previsível	Não determinístico
Menos overhead	Overhead de paralelismo
Melhor para listas pequenas	Melhor para listas grandes

## 🆚 Parallel Stream vs CompletableFuture
Parallel Stream	CompletableFuture
CPU-bound	I/O-bound
Automático	Controlável
Simples	Mais flexível
Pouco configurável	Totalmente configurável
## 🆚 Parallel Stream vs Fork/Join direto

Parallel Stream é abstração de alto nível

Fork/Join é baixo nível

## 👉 Use Parallel Stream quando possível

## ⚠️ Erros comuns

Usar com HTTP / banco

Mutar estado compartilhado

Usar em listas pequenas

Achar que sempre é mais rápido

Usar em ambiente com pouca CPU

## 🧠 Regra de ouro

Parallel Stream é para CPU, não para I/O.

## 🧩 Combina bem com

Strategy: algoritmo do processamento

Factory: escolher tipo de stream

Facade: esconder paralelismo do cliente

Builder: montar pipeline complexo

## 🎯 Resumo mental

Quer paralelismo simples → Parallel Stream

Quer controle de threads → CompletableFuture

Quer I/O → Executor / Virtual Threads

Quer CPU pesada → Fork/Join / Parallel Stream