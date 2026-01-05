
---

# 🧩 Exemplo real — `observer.md`

```md
# Observer Pattern

## 💡 O que é
Permite que múltiplos interessados sejam notificados quando um evento ocorre, de forma desacoplada.

## 🎯 Quando usar
- Pós-processamento (email, auditoria, logs).
- Fluxos extensíveis por plugins.

## ❌ Quando NÃO usar
- Sequência estrita ou quando a ordem é crítica.
- Operações que precisam retornar resultado imediato.

## 🧠 Relação com SOLID / DI
- DIP: publisher não conhece listeners.
- SRP: cada listener faz só uma coisa.

## ⚠️ Armadilhas comuns

Lógica crítica no listener sem garantia transacional.

Listeners síncronos que atrasam resposta; prefira @Async quando apropriado.

## ✅ Checklist arquitetural

 Publisher não chama listeners diretamente?

 Listeners idempotentes e testáveis?

 Usar @TransactionalEventListener se necessário?

## 🧪 Como testar rápido

Publicar evento no contexto de teste e verificar que listeners foram acionados (ou mock do publisher).

## 🧪 Exemplo em Java + Spring
```java
public record OrderCreatedEvent(Long orderId) {}

@Service
public class OrderService {
    private final ApplicationEventPublisher publisher;
    public void create(Order order) {
        // salvar
        publisher.publishEvent(new OrderCreatedEvent(order.getId()));
    }
}

@Component
public class SendEmailListener {
    @EventListener
    public void handle(OrderCreatedEvent event) { /* enviar email */ }
}
