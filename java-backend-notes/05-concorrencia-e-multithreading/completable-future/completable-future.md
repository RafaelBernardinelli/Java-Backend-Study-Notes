# CompletableFuture (Java Concurrency)

## 💡 O que é
`CompletableFuture` é uma abstração de **programação assíncrona** que permite:
- Executar tarefas em background
- Encadear operações
- Combinar resultados
- Tratar erros
Tudo isso **sem bloquear a thread principal**.

Ele resolve o problema clássico de:
- `Future.get()` bloqueante
- Código com callbacks confusos
- Threads mal gerenciadas

---

## 🎯 Quando usar
- Fluxos **I/O-bound**
- Chamadas HTTP assíncronas
- Processamento assíncrono em serviços
- Orquestração de múltiplas tarefas paralelas
- Substituir callbacks e `ExecutorService` manual

**Exemplos reais:**
- Buscar dados em 2 APIs e combinar
- Processar pedido sem bloquear request
- Pipeline assíncrono (validação → cálculo → persistência)

---

## ❌ Quando NÃO usar
- Processamento **CPU-bound pesado** (prefira Fork/Join)
- Quando execução síncrona é simples e clara
- Quando a ordem e o tempo não importam
- Para substituir transações síncronas sem necessidade

---

## 🧠 Relação com CPU-bound vs I/O-bound
- ✔️ Ideal para **I/O-bound**
- ❌ Não é otimizado para CPU-bound pesado

> CompletableFuture **não cria threads mágicas**  
> Ele depende de um `Executor`

---

## 🧠 Relação com SOLID / DI
- **SRP:** cada etapa do pipeline tem uma responsabilidade
- **OCP:** novos passos podem ser adicionados sem alterar os existentes
- **DIP:** depende de abstrações (`Executor`, funções)

---

## ⚠️ Cuidado:

Não use o pool comum para I/O pesado

Prefira injetar um Executor

## 🧵 Execução padrão
Por padrão usa:
```java
ForkJoinPool.commonPool()

🧪 Exemplo básico
CompletableFuture<String> future =
    CompletableFuture.supplyAsync(() -> "resultado");

String result = future.join();

🔗 Encadeamento (thenApply / thenAccept)
CompletableFuture
    .supplyAsync(() -> buscarUsuario())
    .thenApply(usuario -> calcularScore(usuario))
    .thenAccept(score -> salvarScore(score));

🔀 Execução paralela
CompletableFuture<User> userFuture = buscarUsuarioAsync();
CompletableFuture<Order> orderFuture = buscarPedidoAsync();

CompletableFuture
    .allOf(userFuture, orderFuture)
    .thenRun(() -> {
        User u = userFuture.join();
        Order o = orderFuture.join();
        processar(u, o);
    });

➕ Combinar resultados
CompletableFuture<Integer> total =
    precoAsync()
        .thenCombine(freteAsync(), Integer::sum);

🚨 Tratamento de erro
CompletableFuture
    .supplyAsync(() -> chamadaExterna())
    .exceptionally(ex -> {
        log.error("Erro", ex);
        return fallback();
    });


Ou:

.handle((result, ex) -> ex != null ? fallback() : result)

🧵 Usando Executor customizado
Executor executor = Executors.newFixedThreadPool(10);

CompletableFuture
    .supplyAsync(() -> chamadaExterna(), executor);
``` 

## ✔️ Boa prática
## ❌ Evite usar pool comum para I/O

## 🆚 CompletableFuture vs ExecutorService
ExecutorService	CompletableFuture
Baixo nível	Alto nível
Código verboso	Código fluente
Controle manual	Pipeline funcional
Bloqueante	Não bloqueante
## 🆚 CompletableFuture vs Reactive (WebFlux)

CompletableFuture → assíncrono imperativo

Reactive → assíncrono reativo e não-bloqueante

## 👉 CompletableFuture é mais simples e suficiente na maioria dos casos

## ⚠️ Erros comuns

Usar join() cedo demais

Não tratar exceções

Usar ForkJoinPool para I/O

Criar new Thread() dentro do pipeline

## 🧠 Regra de ouro

CompletableFuture não é sobre thread.
É sobre fluxo assíncrono.

## 🧩 Padrões que se combinam bem

Factory: escolher qual fluxo executar

Strategy: definir comportamento da etapa

Facade: expor um método síncrono que usa async internamente

Observer: reagir ao término de futures

## 🎯 Resumo mental

Quer não bloquear? → CompletableFuture

Quer paralelismo simples? → CompletableFuture

Quer pipeline claro? → CompletableFuture

Quer CPU pesada? → Fork/Join