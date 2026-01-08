
---

## 🧵 `cached-thread-pool.md`

```md
# CachedThreadPool

## ❓ Pergunta que responde
👉 Quero threads criadas **sob demanda**?

## 💡 O que é
Cria threads conforme necessário e reutiliza threads ociosas.
⚠️ Não possui limite máximo.

## 🎯 Quando usar
- Tarefas rápidas
- Curta duração
- Baixo volume imprevisível

## ❌ Quando NÃO usar
- Sistemas críticos
- Ambientes com carga variável alta

## ⚠️ Armadilhas

Pode criar milhares de threads

Alto risco de exaustão de recursos

## ✅ Checklist

 Volume controlado?

 Ambiente tolera picos?

## 🧪 Exemplo em Java
```java
ExecutorService executor = Executors.newCachedThreadPool();
executor.submit(() -> task());
