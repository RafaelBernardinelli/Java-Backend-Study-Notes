
---

# 🧩 Exemplo real — `strategy.md`

```md
# Strategy Pattern

## 💡 O que é
Define uma família de algoritmos/estratégias intercambiáveis e permite selecionar em tempo de execução.

## 🎯 Quando usar
- Regras que mudam frequentemente (descontos, cálculos).
- Evitar grandes `if/else`.

## ❌ Quando NÃO usar
- Apenas uma regra possível.
- Regras simples que não se repetem.

## 🧠 Relação com SOLID / DI
- OCP: adicione nova estratégia sem tocar no cliente.
- DIP: cliente depende da interface da estratégia.

## ⚠️ Armadilhas comuns

Estratégias com estado mutável.

Associação frágil por nome/classe (usar enum ou método supports).

## ✅ Checklist arquitetural

 Estratégias stateless?

 Mapeamento claro (enum ou qualifier)?

 Cliente lida com estratégia ausente?

## 🧪 Como testar rápido

Mockar lista de strategies e validar a escolha e o resultado.

## 🧪 Exemplo em Java + Spring
```java
public enum DiscountType { NONE, COUPON, BLACK_FRIDAY }

public interface DiscountStrategy {
    BigDecimal apply(BigDecimal value);
    DiscountType supports();
}

@Service
public class CouponDiscount implements DiscountStrategy {
    public BigDecimal apply(BigDecimal value) { return value.subtract(BigDecimal.valueOf(10)); }
    public DiscountType supports() { return DiscountType.COUPON; }
}

@Service
public class DiscountService {
    private final Map<DiscountType, DiscountStrategy> strategies;
    public DiscountService(List<DiscountStrategy> list) {
        this.strategies = list.stream().collect(Collectors.toMap(DiscountStrategy::supports, s -> s));
    }
    public BigDecimal apply(DiscountType type, BigDecimal value) {
        return strategies.get(type).apply(value);
    }
}
