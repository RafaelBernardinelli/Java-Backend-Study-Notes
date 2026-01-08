
---

## 🧵 `fixed-thread-pool.md`

```md
# FixedThreadPool

## ❓ Pergunta que responde
👉 Quantas threads **no máximo** posso usar?

## 💡 O que é
Pool com número fixo de threads.
Tarefas excedentes entram em fila.

## 🎯 Quando usar
- Backends tradicionais
- Processamento controlado
- Limitar consumo de CPU

## ❌ Quando NÃO usar
- Picos imprevisíveis muito altos
- Tarefas bloqueantes longas

## ⚠️ Armadilhas

Fila infinita pode causar OOM

Número de threads mal dimensionado

## ✅ Checklist

 Pool dimensionado?

 Tarefas CPU ou I/O?

 Monitoramento de fila?

## 🧪 Exemplo em Java
```java
ExecutorService executor = Executors.newFixedThreadPool(4);

executor.submit(() -> task());
executor.shutdown();
