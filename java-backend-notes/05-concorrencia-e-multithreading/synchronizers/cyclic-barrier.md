
---

## 🔄 `cyclic-barrier.md`

```md
# CyclicBarrier

## ❓ Pergunta que responde
👉 Threads precisam **se encontrar**?

## 💡 O que é
Bloqueia threads até todas chegarem a um ponto comum.
É **reutilizável**.

## 🎯 Quando usar
- Processamento em etapas
- Simulações
- Paralelismo 

## ⚠️ Armadilhas

Deadlock se uma thread não chegar

## 🧪 Exemplo
```java
CyclicBarrier barrier = new CyclicBarrier(3);

barrier.await();
