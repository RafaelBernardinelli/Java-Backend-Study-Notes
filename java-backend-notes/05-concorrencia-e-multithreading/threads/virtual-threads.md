
---

## 🧵 `virtual-threads.md`

```md
# Virtual Threads (Java 21+)

## ❓ Pergunta que responde
👉 Quero escalar milhares de tarefas concorrentes?

## 💡 O que é
Threads leves (Project Loom).
Excelente para I/O-bound.

## 🎯 Quando usar
- APIs REST
- Chamadas HTTP
- Sistemas altamente concorrentes

## ❌ Quando NÃO usar

Java < 21

CPU-bound pesado sem controle

## ⚠️ Armadilhas

Ainda exige controle de recursos externos

Não substitui design ruim

## ✅ Checklist

 Java 21+?

 I/O-bound?

## 🧪 Exemplo em Java
```java
ExecutorService executor =
    Executors.newVirtualThreadPerTaskExecutor();

executor.submit(() -> callExternalApi());
