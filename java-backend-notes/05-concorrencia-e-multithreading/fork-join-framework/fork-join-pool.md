# ForkJoinPool

## ❓ Pergunta que responde
👉 Como gerenciar threads para paralelismo massivo?

## 💡 O que é
Pool especializado que utiliza **work-stealing**:
threads ociosas roubam tarefas de outras threads.

## 🎯 Características
- Número de threads ≈ núcleos da CPU
- Baixa contenção
- Alta eficiência

## ⚠️ Armadilhas

Bloqueios degradam o pool

Não usar para I/O

## 🧪 Exemplo
```java
ForkJoinPool pool = new ForkJoinPool();

pool.submit(() -> heavyTask());
pool.shutdown();
