# CountDownLatch

## ❓ Pergunta que responde
👉 Preciso esperar **N eventos** acontecerem?

## 💡 O que é
Bloqueia threads até que um contador chegue a zero.
É **uso único**.

## 🎯 Quando usar
- Esperar inicializações
- Testes paralelos
- Sincronização simples

## ❌ Quando NÃO usar

Coordenação reutilizável

## ⚠️ Armadilhas

Não pode ser reutilizado

## 🧪 Exemplo
```java
CountDownLatch latch = new CountDownLatch(3);

executor.submit(() -> latch.countDown());
latch.await();
