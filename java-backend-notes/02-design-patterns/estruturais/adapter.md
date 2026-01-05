
---

# 🧩 Exemplo real — `adapter.md`

```md
# Adapter Pattern

## 💡 O que é
Adapta uma interface existente para outra esperada pelo cliente, sem mudar o legado.

## 🎯 Quando usar
- Integração com APIs/SDKs legados.
- Unificar interfaces distintas sob uma abstração comum.

## ❌ Quando NÃO usar
- Quando você pode mudar ambos os lados (legacy + novo).
- Quando a adaptação adiciona lógica de negócio.

## 🧠 Relação com SOLID / DI
- DIP: clientes dependem de abstração, adapter implementa essa abstração.
- SRP: adapter apenas converte/transforma.

## ⚠️ Armadilhas comuns

Colocar lógica de negócio no adapter (adapter deve converter/encaminhar).

Adapter com muitos métodos (sinal de design ruim).

## ✅ Checklist arquitetural

 Adapter só transforma/encaminha?

 Tests de conversão limpos?

 Adapter registrado como bean para DI?

## 🧪 Como testar rápido

Mockar LegacyClient e verificar chamada com valor convertido.

## 🧪 Exemplo em Java + Spring
```java
public interface PaymentGateway { void pay(BigDecimal value); }

// Legado
public class LegacyClient { public void makePayment(double v) { ... } }

@Component
public class LegacyPaymentAdapter implements PaymentGateway {
    private final LegacyClient client;
    public LegacyPaymentAdapter(LegacyClient client) { this.client = client; }
    public void pay(BigDecimal value) { client.makePayment(value.doubleValue()); }
}
