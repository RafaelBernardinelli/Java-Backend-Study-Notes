# 🧠 Mapa Mental — Design Patterns (visão arquitetural)

> Cada pattern existe para responder **uma pergunta específica de design**.  
> Se você sabe a pergunta, você sabe o pattern.

---

## 🔒 Singleton  
**Pergunta que responde:**  
👉 *Quantas instâncias devem existir?*

**Ideia central:**  
Garantir uma única instância compartilhada.

**No Spring:**  
- Beans são `singleton` por padrão  
- Usado em `@Service`, `@Repository`, `@Component`

---

## 🏭 Factory  
**Pergunta que responde:**  
👉 *Qual objeto usar?*

**Ideia central:**  
Centralizar a escolha da implementação correta.

**Exemplo típico:**  
- Tipo de pagamento  
- Tipo de cálculo  
- Tipo de integração

---

## 🎯 Strategy  
**Pergunta que responde:**  
👉 *Como executar?*

**Ideia central:**  
Algoritmos intercambiáveis para executar uma ação.

**Exemplo típico:**  
- Cálculo de juros  
- Desconto  
- Validação de regras

---

## 👂 Observer  
**Pergunta que responde:**  
👉 *Quem reage ao evento?*

**Ideia central:**  
Notificar múltiplos interessados quando algo acontece.

**No Spring:**  
- `ApplicationEventPublisher`
- `@EventListener`

---

## 🧱 Builder  
**Pergunta que responde:**  
👉 *Como construir?*

**Ideia central:**  
Construir objetos complexos passo a passo.

**Exemplo típico:**  
- DTOs grandes  
- Objetos imutáveis  
- Requests complexos

---

## 🧬 Prototype  
**Pergunta que responde:**  
👉 *Sempre preciso de uma nova instância?*

**Ideia central:**  
Criar uma nova instância a cada solicitação.

**No Spring:**  
- `@Scope("prototype")`
- Uso com `ObjectProvider`

---

## 🔌 Adapter  
**Pergunta que responde:**  
👉 *Como integrar?*

**Ideia central:**  
Adaptar uma interface existente para outra esperada.

**Exemplo típico:**  
- APIs legadas  
- SDKs externos  
- Sistemas terceiros

---

## 🧩 Decorator  
**Pergunta que responde:**  
👉 *Como estender comportamento?*

**Ideia central:**  
Adicionar responsabilidades dinamicamente sem alterar a classe original.

**Exemplo típico:**  
- Taxas  
- Juros  
- Logs  
- Validações encadeadas

---

## 🛡️ Proxy  
**Pergunta que responde:**  
👉 *Como controlar acesso?*

**Ideia central:**  
Controlar ou interceptar chamadas a um objeto.

**No Spring:**  
- `@Transactional`
- `@Cacheable`
- `@Secured`

---

## 🧱 Facade  
**Pergunta que responde:**  
👉 *Como simplificar o uso de um sistema complexo?*

**Ideia central:**  
Fornecer uma **interface única e simples** para um conjunto de subsistemas.

**Exemplo típico:**  
- `OrderFacade`
- `PaymentFacade`
- Camada Application Service (DDD)
- BFF (Backend for Frontend)

---

## 🧠 Regra de Ouro (entrevista & arquitetura)

> ❌ Não escolha o pattern pelo nome  
> ✅ Escolha o pattern pela **pergunta que você precisa responder**

---

## 🎯 Dica prática de arquiteto
- Muitos serviços no controller → **Facade**
- Muitos `if/else` → **Strategy ou Factory**
- Criação confusa → **Builder**
- Integração feia → **Adapter**
- Lógica antes/depois → **Proxy**
- Regras encadeadas → **Decorator**
