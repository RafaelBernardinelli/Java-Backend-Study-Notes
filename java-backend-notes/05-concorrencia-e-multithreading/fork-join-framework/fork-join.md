# Fork/Join Framework — Java

## 💡 O que é
Framework de paralelismo introduzido no Java 7
para **dividir grandes tarefas em subtarefas menores**
e executá-las em paralelo.

Baseado no princípio:
> Divide and Conquer

---

## ❓ Problema que resolve
👉 Como paralelizar tarefas **CPU-bound** de forma eficiente?

---

## 🧠 Componentes principais

| Componente | Papel |
|----------|------|
| ForkJoinPool | Pool especializado |
| RecursiveTask | Retorna resultado |
| RecursiveAction | Não retorna resultado |
| Work-Stealing | Balanceamento automático |

---

## 🎯 Quando usar
- Algoritmos recursivos (work-stealing e divider-concurre     )
- Processamento pesado de CPU
- Grandes volumes de dados

## ❌ Quando NÃO usar
- I/O bloqueante
- Chamadas remotas
- Esperas longas

---

## 🧠 Regra de ouro
> Fork/Join é para **CPU**, não para I/O

# Dividir(processamento) pra conquistar
