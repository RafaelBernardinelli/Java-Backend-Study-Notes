# SingleThreadExecutor

## ❓ Pergunta que responde
👉 Preciso garantir execução **sequencial e ordenada**?

## 💡 O que é
Executor que utiliza **apenas uma thread** para executar tarefas.
Se a thread falhar, outra é criada automaticamente.

## 🎯 Quando usar
- Escrita em arquivo
- Processamento sequencial
- Garantia de ordem
- Evitar concorrência em recursos compartilhados

## ❌ Quando NÃO usar
- Tarefas lentas ou bloqueantes
- Processamento pesado
- Alta taxa de requisições

## ⚠️ Armadilhas

Fila pode crescer indefinidamente

Uma tarefa lenta bloqueia todas as outras

## ✅ Checklist

 Ordem é obrigatória?

 Tarefas são rápidas?

 Executor é finalizado?

## 🧪 Exemplo em Java
```java
ExecutorService executor = Executors.newSingleThreadExecutor();

executor.submit(() -> process());
executor.shutdown();
