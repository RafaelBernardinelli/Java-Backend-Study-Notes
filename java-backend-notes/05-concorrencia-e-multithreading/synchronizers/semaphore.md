
---

## 🚦 `semaphore.md`

```md
# Semaphore

## ❓ Pergunta que responde
👉 Quantas threads podem acessar um recurso?

## 💡 O que é
Controla acesso concorrente por permissões.

## 🎯 Quando usar
- Pool de conexões
- Rate limiting
- Recursos limitados

## ⚠️ Armadilhas

Esquecer release()

## 🧪 Exemplo
```java
Semaphore semaphore = new Semaphore(2);

semaphore.acquire();
try {
    use();
} finally {
    semaphore.release();
}
