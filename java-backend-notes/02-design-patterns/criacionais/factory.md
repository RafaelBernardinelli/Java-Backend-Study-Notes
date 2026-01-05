
---

# 🧩 Exemplo real — `factory.md`

```md
# Factory Pattern

## 💡 O que é
Encapsula a **lógica de seleção/instanciação** de implementações, desacoplando quem usa da criação.

## 🎯 Quando usar
- Múltiplas implementações (drivers, processadores).
- Decisão por enum/config/tenant.

## ❌ Quando NÃO usar
- Só existe uma implementação.
- Criação trivial sem lógica.

## 🧠 Relação com SOLID / DI
- OCP: novas implementações sem modificar consumidor.
- DIP: consumidores dependem de abstrações, factory decide a implementação.

## ⚠️ Armadilhas comuns

- Usar new dentro da factory (perde DI/AOP).

- Lógica de negócio dentro da factory.

## ✅ Checklist arquitetural

- Factory não instancia com new.

- Factory é simples e testável.

- Extensível adicionando novos beans.

## 🧪 Como testar rápido

- Registrar um fake PaymentProcessor e garantir que a factory o devolve pelo PaymentType.

## 🧪 Exemplo em Java + Spring
```java
public enum PaymentType { PIX, CARD }

public interface PaymentProcessor { void process(); PaymentType supports(); }

@Service
public class PaymentProcessorFactory {
    private final Map<PaymentType, PaymentProcessor> map;
    public PaymentProcessorFactory(List<PaymentProcessor> list) {
        this.map = list.stream().collect(Collectors.toMap(PaymentProcessor::supports, p -> p));
    }
    public PaymentProcessor get(PaymentType type) {
        return map.get(type);
    }
}
