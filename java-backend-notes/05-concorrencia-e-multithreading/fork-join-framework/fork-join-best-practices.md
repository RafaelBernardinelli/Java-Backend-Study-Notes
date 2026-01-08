
---

## ⚠️ `fork-join-best-practices.md`

```md
# Fork/Join — Boas práticas e armadilhas

## ✅ Boas práticas
- Tarefas CPU-bound
- Divisão equilibrada
- Usar join corretamente
- Tarefas imutáveis

## ❌ Armadilhas comuns
- I/O bloqueante
- Tasks grandes demais
- Tasks pequenas demais
- Deadlocks acidentais

## 🧠 Comparações importantes
- Fork/Join vs ExecutorService
- Fork/Join vs Parallel Streams

## 🎯 Regra final
> Fork/Join é poderoso, mas só quando o problema pede.

## 🧠 Dica de arquiteto
Se você usa Fork/Join para chamadas HTTP,
você está usando o framework errado.
