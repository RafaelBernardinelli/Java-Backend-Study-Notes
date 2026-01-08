# Concurrent Collections — Java

## 💡 O que são
As *Concurrent Collections* fazem parte do pacote
`java.util.concurrent` e fornecem **estruturas de dados thread-safe**
com **melhor performance** do que `Collections.synchronized*`.

Elas utilizam:
- Lock striping
- Algoritmos lock-free
- CAS (Compare-And-Swap)

---

## ❌ O que NÃO usar em concorrência
- `ArrayList`
- `HashMap`
- `HashSet`
- `Collections.synchronizedList(...)`

👉 Esses bloqueiam demais ou geram bugs sutis.

---

## 🧠 Mapa mental — Pergunta que cada coleção responde

| Coleção | Pergunta que responde |
|------|----------------|
| ConcurrentHashMap | Múltiplas threads escrevendo/lendo? |
| CopyOnWriteArrayList | Muitas leituras, poucas escritas? |
| CopyOnWriteArraySet | Conjunto imutável na prática? |
| ConcurrentLinkedQueue | Fila não bloqueante? |
| ConcurrentLinkedDeque | Fila dupla concorrente? |
| BlockingQueue | Preciso bloquear até ter dado? |
| DelayQueue | Processar no futuro? |
| PriorityBlockingQueue | Processar por prioridade? |

---

## 🧠 Regra de ouro
> ❌ Sincronizar tudo  
> ✅ Escolher a coleção certa
