# Synchronizers — Java Concurrency

## 💡 O que são
*Synchronizers* são utilitários do pacote
`java.util.concurrent` usados para **coordenação entre threads**.

Eles **não armazenam dados** (como collections),
mas controlam **quando threads podem prosseguir**.

---

## ❌ O que NÃO são
- Não são collections
- Não são executors
- Não substituem design ruim

---

## 🧠 Mapa mental — Pergunta que cada synchronizer responde

| Synchronizer | Pergunta que responde |
|------------|----------------|
| CountDownLatch | Esperar eventos acontecerem? |
| CyclicBarrier | Sincronizar grupos? |
| Semaphore | Limitar acesso concorrente? |
| Exchanger | Trocar dados entre threads? |
| Phaser | Coordenação em fases? |
| Lock / Condition | Controle manual de concorrência? |
| ReadWriteLock | Mais leitura que escrita? |

---

## 🧠 Regra de ouro
> ❌ Sincronizar tudo  
> ✅ Coordenar apenas o necessário
