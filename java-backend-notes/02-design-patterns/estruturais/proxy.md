
---

# 🧩 Exemplo real — `proxy.md`

```md
# Proxy Pattern

## 💡 O que é
Objeto que controla acesso a outro objeto, adicionando comportamento (caching, segurança, logs, transações).

## 🎯 Quando usar
- Cross-cutting concerns (transação, cache, segurança).
- Controlar criação/execução de chamadas.

## ❌ Quando NÃO usar
- Quando a lógica pertence à própria implementação.
- Quando proxy adiciona demasiada complexidade.

## 🧠 Relação com SOLID / DI
- DIP: cliente chama a abstração; o container pode fornecer proxy.
- OOP: proxy mantém mesmo contrato da classe real.

## ⚠️ Armadilhas comuns

Chamar método anotado com @Transactional internamente na mesma classe (proxy não intercepta).

Confundir proxy com decorator (objetivos similares, mas proxy controla acesso).

## ✅ Checklist arquitetural

 Conhece limitações de proxy (self-invocation)?

 Cross-cutting concerns isolados?

 Testes que cobrem comportamento adicional?

## 🧪 Como testar rápido

Verificar que método anotado é envolvido pelo comportamento (ex.: transação aberta).

## 🧪 Exemplo em Java + Spring
```java
@Service
public class PaymentService {
    @Transactional
    public void pay() { /* ... */ }
}

Spring cria proxy que adiciona comportamento transacional. Outra forma: criar proxy manual:

public class LoggingProxy implements PaymentService {
    private final PaymentService delegate;
    public void pay() {
        log.info("before");
        delegate.pay();
        log.info("after");
    }
}
