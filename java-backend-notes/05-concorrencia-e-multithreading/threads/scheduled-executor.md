
---

## ⏰ `scheduled-executor.md`

```md
# ScheduledExecutorService

## ❓ Pergunta que responde
👉 Preciso executar algo **no futuro ou periodicamente**?

## 💡 O que é
Executor especializado em tarefas agendadas.

## 🎯 Quando usar
- Jobs periódicos
- Retry com delay
- Heartbeats

## ❌ Quando NÃO usar

Processamento pesado

Substituir sistemas de scheduler dedicados

## ⚠️ Armadilhas

Jobs longos acumulam atrasos

Falta de monitoramento

## ✅ Checklist

 Job é idempotente?

 Pool suficiente?

## 🧪 Exemplo em Java
```java
ScheduledExecutorService scheduler =
    Executors.newScheduledThreadPool(2);

scheduler.scheduleAtFixedRate(
    () -> job(),
    0, 10, TimeUnit.SECONDS
);

scheduler.scheduleIsFixedDelay( )
