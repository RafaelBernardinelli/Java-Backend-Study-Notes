
---

# 🧩 Exemplo real — `builder.md`

```md
# Builder Pattern

## 💡 O que é
Padroniza a criação de objetos complexos/imutáveis, com API fluente.

## 🎯 Quando usar
- Muitos campos, muitos opcionais.
- Objetos imutáveis / value objects.

## ❌ Quando NÃO usar
- Objetos pequenos e triviais.
- Services ou beans gerenciados pelo container (não é escopo).

## 🧠 Relação com SOLID / DI
- SRP: separa construção da lógica.
- DIP: consumidores usam interfaces/DTOs criados pelo builder.

## ⚠️ Armadilhas comuns

Validar apenas depois do build() sem mensagens claras.

Usar Builder para classes que deveriam ser simples DTOs com construtor.

## ✅ Checklist arquitetural

 build() valida obrigatórios?

 Objeto imutável após criação?

 Sem lógica de negócio no builder?

## 🧪 Como testar rápido

Testar caminhos válidos e inválidos do build() (faltando campos obrigatórios).

## 🧪 Exemplo em Java (Lombok opcional)
```java
@Builder
public class Order {
    private final Long id;
    private final String customer;
    private final BigDecimal total;
    private final String notes;
}

Order o = Order.builder().id(1L).customer("R").total(BigDecimal.TEN).build();

