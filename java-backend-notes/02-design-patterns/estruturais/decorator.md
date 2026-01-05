# Decorator Pattern

## 💡 O que é
Permite **adicionar comportamentos a um objeto dinamicamente**,
sem alterar sua classe original, envolvendo-o com outros objetos
que implementam a mesma interface.

## 🎯 Quando usar
- Regras encadeadas (taxas, juros, descontos, validações)
- Processamento em pipeline
- Quando herança causaria explosão de subclasses
- Combinar comportamentos em tempo de execução

## ❌ Quando NÃO usar
- Uma única regra simples
- Quando um `if/else` é mais claro e estável
- Quando a ordem dos comportamentos não importa ou não pode variar

## 🧠 Relação com SOLID / DI
- **OCP**: adiciona comportamento sem modificar classes existentes
- **SRP**: cada decorator tem uma responsabilidade única
- **DIP**: cliente depende de abstração, não da implementação concreta

## ⚠️ Armadilhas comuns

Muitos decorators aninhados sem clareza

Dependência da ordem dos decorators sem documentação

Confundir Decorator com Proxy

Proxy controla acesso

Decorator adiciona comportamento

## ✅ Checklist arquitetural

 Todos os decorators implementam a mesma interface?

 Cada decorator tem apenas uma responsabilidade?

 Ordem dos decorators é clara e previsível?

 Sem lógica de negócio no cliente?

## 🧪 Como testar rápido

Testar cada decorator isoladamente

Testar combinações e ordens diferentes

Garantir que BaseCharge funciona sem decorators

## 🧠 Quando pensar em outro padrão

Muitas escolhas de algoritmo → Strategy

Criação complexa → Builder

Lógica antes/depois do método → Proxy

## 🧪 Exemplo em Java + Spring

Interface base:
```java
public interface Charge {
    BigDecimal calculate();
}

Implementação principal:

public class BaseCharge implements Charge {
    private final BigDecimal value;

    public BaseCharge(BigDecimal value) {
        this.value = value;
    }

    @Override
    public BigDecimal calculate() {
        return value;
    }
}


Decorator abstrato:

public abstract class ChargeDecorator implements Charge {
    protected final Charge charge;

    protected ChargeDecorator(Charge charge) {
        this.charge = charge;
    }
}


Decorator de taxa:

public class FeeDecorator extends ChargeDecorator {
    public FeeDecorator(Charge charge) {
        super(charge);
    }

    @Override
    public BigDecimal calculate() {
        return charge.calculate().add(BigDecimal.valueOf(5));
    }
}


Decorator de desconto:

public class DiscountDecorator extends ChargeDecorator {
    public DiscountDecorator(Charge charge) {
        super(charge);
    }

    @Override
    public BigDecimal calculate() {
        return charge.calculate().subtract(BigDecimal.valueOf(3));
    }
}


Uso:

Charge charge =
    new DiscountDecorator(
        new FeeDecorator(
            new BaseCharge(BigDecimal.valueOf(100))
        )
    );

BigDecimal total = charge.calculate(); // 102

🔁 Decorator com Spring (composição dinâmica)
@Service
public class ChargeBuilder {
    public Charge build(BigDecimal baseValue, boolean fee, boolean discount) {
        Charge charge = new BaseCharge(baseValue);

        if (fee) {
            charge = new FeeDecorator(charge);
        }
        if (discount) {
            charge = new DiscountDecorator(charge);
        }
        return charge;
    }
}