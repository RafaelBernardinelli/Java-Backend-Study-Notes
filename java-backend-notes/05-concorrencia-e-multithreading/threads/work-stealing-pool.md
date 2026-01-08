
---

## 🧵 `work-stealing-pool.md`

```md
# WorkStealingPool (ForkJoinPool)

## ❓ Pergunta que responde
👉 Quero paralelismo máximo automaticamente?

## 💡 O que é
Pool baseado em Fork/Join.
Threads roubam tarefas umas das outras.

## 🎯 Quando usar
- Processamento CPU-bound
- Algoritmos paralelos
- Streams paralelos

## ❌ Quando NÃO usar

Tarefas bloqueantes (I/O)

Chamadas remotas

## ⚠️ Armadilhas

Bloqueio degrada desempenho

Difícil de debugar

## ✅ Checklist

 CPU-bound?

 Sem I/O bloqueante?

## 🧪 Exemplo em Java
```java
ExecutorService executor =
    Executors.newWorkStealingPool();

executor.submit(() -> task());
