# Facade Pattern

## 💡 O que é
Fornece uma **interface simples e unificada** para um conjunto
complexo de subsistemas, escondendo detalhes de implementação
e reduzindo o acoplamento do cliente.

## 🎯 Quando usar
- Fluxos complexos com muitos serviços envolvidos
- Orquestração de regras de negócio
- APIs internas para uso por controllers ou outros módulos
- Evitar que camadas superiores conheçam detalhes internos

## ❌ Quando NÃO usar
- Quando o fluxo é simples (1 ou 2 chamadas diretas)
- Quando a facade vira um “god class”
- Para encapsular lógica que deveria estar em domain services

## 🧠 Relação com SOLID / DI
- **SRP**: facade orquestra, serviços executam
- **DIP**: clientes dependem da facade, não dos subsistemas
- **ISP**: expõe apenas o necessário para o cliente

## ⚠️ Armadilhas comuns
Facade com regras de negócio complexas demais

Facade chamando repositórios diretamente

Criar facade para tudo sem necessidade

## ✅ Checklist arquitetural
 Facade apenas orquestra?

 Serviços internos fazem o trabalho pesado?

 Controller não conhece detalhes do fluxo?

 Facade é testável isoladamente?

## 🧪 Como testar rápido
Mockar os serviços internos

Verificar a ordem das chamadas

Garantir que erros são propagados corretamente

## 🧠 Comparações importantes
- Facade vs Service

  - Service executa regra

  - Facade coordena várias regras

- Facade vs Adapter

  - Adapter muda interface

  - Facade simplifica uso

- Facade vs Mediator

  - Facade é entrada única

  - Mediator coordena comunicação bidirecional

📌 Exemplo real de mercado
OrderFacade, PaymentFacade, PixFacade

Camada Application Service em DDD

BFF (Backend for Frontend)

## 🧪 Exemplo em Java + Spring

Serviços internos (subsistemas):
```java
@Service
public class InventoryService {
    public void reserve(Long productId) { }
}

@Service
public class PaymentService {
    public void charge(BigDecimal amount) { }
}

@Service
public class ShippingService {
    public void schedule(Long orderId) { }
}
Facade:

@Service
public class OrderFacade {

    private final InventoryService inventoryService;
    private final PaymentService paymentService;
    private final ShippingService shippingService;

    public OrderFacade(
        InventoryService inventoryService,
        PaymentService paymentService,
        ShippingService shippingService
    ) {
        this.inventoryService = inventoryService;
        this.paymentService = paymentService;
        this.shippingService = shippingService;
    }

    public void placeOrder(Long productId, BigDecimal amount) {
        inventoryService.reserve(productId);
        paymentService.charge(amount);
        shippingService.schedule(productId);
    }
}
Controller usando a Facade:

@RestController
@RequestMapping("/orders")
public class OrderController {

    private final OrderFacade orderFacade;

    public OrderController(OrderFacade orderFacade) {
        this.orderFacade = orderFacade;
    }

    @PostMapping
    public void createOrder() {
        orderFacade.placeOrder(1L, BigDecimal.valueOf(100));
    }
}