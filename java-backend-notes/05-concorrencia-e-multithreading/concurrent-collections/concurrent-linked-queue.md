
---

## 📥 `concurrent-linked-queue.md`

```md
# ConcurrentLinkedQueue

## ❓ Pergunta que responde
👉 Preciso de fila não bloqueante?

## 💡 O que é
Fila baseada em algoritmo lock-free.
Não bloqueia threads.

## 🎯 Quando usar
- Eventos
- Filas leves
- Comunicação entre threads

## ❌ Quando NÃO usar

Quando precisa bloquear esperando elemento

## 🧪 Exemplo
```java
Queue<String> queue = new ConcurrentLinkedQueue<>();
queue.offer("msg");
queue.poll();
