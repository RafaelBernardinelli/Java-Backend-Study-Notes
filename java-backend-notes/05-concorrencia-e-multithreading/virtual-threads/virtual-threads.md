Passa a ser gerenciada 100% pela JVM e não pelo sistema operacional, as threads tradicionais são recursos em cima do sistema operacional, portanto, são limitadas.

Executar um numero muito alto de tarefas concorrente, com overhead (custo operacional) muito baixo

Quando alocamentos uma virtual thread, não estamos mais alocando uma thread do sistema operacional, ela só vai existir dentro da JVM

Simplifica a programação concorrente

Aumentar o desempenho das respostas da aplicação

Reduz a complexidade das extrategias de utilizar thread pools, pois a JVM ja gerencia pra nós.

# Virtual Threads (Project Loom – Java)

## 💡 O que é
Virtual Threads são threads **leves**, gerenciadas **100% pela JVM**  
e **não pelo sistema operacional**.

Diferente das threads tradicionais (plataforma), que são recursos caros
e limitados do SO, as Virtual Threads existem apenas **dentro da JVM**.

> Uma Virtual Thread **não é** uma thread do sistema operacional.

---

## 🧠 Diferença fundamental
### Threads tradicionais (Platform Threads)
- Mapeadas 1:1 com threads do SO
- Caras (memória + contexto)
- Limitadas em quantidade
- Gerenciadas pelo sistema operacional

### Virtual Threads
- Gerenciadas pela JVM
- Não consomem thread do SO enquanto estão bloqueadas
- Milhões podem existir
- Overhead extremamente baixo

---

## 🎯 Quando usar
- Aplicações **I/O-bound**
- APIs REST
- Microserviços
- Chamadas HTTP
- Banco de dados
- Mensageria
- Processamento concorrente massivo

**Exemplos reais:**
- 10k+ requisições simultâneas
- Cada request faz chamadas externas
- Código imperativo tradicional

---

## ❌ Quando NÃO usar
- Processamento **CPU-bound pesado**
- Algoritmos matemáticos
- Fork/Join
- Parallel Streams
- Cálculos intensivos

> Virtual Threads **não aceleram CPU**, apenas **escala concorrência**

---

## 🧠 Relação com CPU-bound vs I/O-bound
- ✔️ Excelente para **I/O-bound**
- ❌ Não indicada para **CPU-bound**

Por quê?
- Virtual Threads brilham quando **bloqueiam**
- CPU-bound não bloqueia → não há ganho

---

## 🧵 Como funcionam internamente (conceito)
- Virtual Threads são executadas sobre poucas **Platform Threads**
- Quando uma Virtual Thread bloqueia (I/O):
  - A JVM a suspende
  - Libera a thread do SO
  - Executa outra Virtual Thread

👉 Isso se chama **mount / unmount**

---

## 🧪 Exemplo básico
```java
Thread.startVirtualThread(() -> {
    System.out.println("Rodando em Virtual Thread");
});
🧪 Executor com Virtual Threads

ExecutorService executor =
    Executors.newVirtualThreadPerTaskExecutor();

executor.submit(() -> {
    chamadaHttp();
});

```
✔️ Um task = uma Virtual Thread
✔️ Sem pool fixo
✔️ Sem tuning complexo

## 🧠 Simplificação da concorrência
Antes (threads tradicionais):

Pool fixo

Fila

Rejeição

Tuning manual

Agora:

Uma Virtual Thread por tarefa

JVM gerencia tudo

Código simples

Escala massivamente

## 🧠 Relação com SOLID / Design
SRP: código de negócio sem lógica de concorrência

OCP: troca de modelo de execução sem alterar lógica

DIP: depende de Executor, não de implementação

Clean Code: menos infraestrutura visível

## 🆚 Virtual Threads vs ExecutorService tradicional
Executor tradicional	Virtual Threads
Pool limitado	Milhares/milhões
Configuração manual	JVM gerencia
Threads caras	Threads leves
Fácil esgotar	Difícil esgotar

## 🆚 Virtual Threads vs CompletableFuture
Virtual Threads → assíncrono bloqueante

CompletableFuture → assíncrono não-bloqueante

## 👉 Virtual Threads permitem escrever:


String r1 = chamada1();
String r2 = chamada2();
Sem bloquear threads do SO.

## 🆚 Virtual Threads vs Reactive (WebFlux)
Virtual Threads → código imperativo simples

Reactive → paradigma reativo complexo

## 👉 Virtual Threads reduzem a necessidade de Reactive
em muitos cenários

## ⚠️ Limitações importantes
Ainda usam Platform Threads por baixo

Não tornam CPU infinita

Bibliotecas nativas bloqueantes podem limitar ganhos

Não substituem Fork/Join

## 🚨 Erros comuns
Usar para CPU-bound

Misturar com parallelStream

Achar que substitui todo tipo de concorrência

Ignorar limites de banco / APIs externas

## 🧠 Regra de ouro
Virtual Threads escalam espera, não CPU.

## 🧩 Combina muito bem com
Facade: esconder concorrência

Factory: escolher executor

Strategy: decidir modelo de execução

Observer: reagir a eventos assíncronos

## 🎯 Resumo mental
Muitas tarefas? → Virtual Threads

Muito I/O? → Virtual Threads

Código simples? → Virtual Threads

CPU pesada? → Fork/Join