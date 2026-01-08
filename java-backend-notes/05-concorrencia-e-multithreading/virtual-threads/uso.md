## ✅ Ativar Virtual Threads no Spring Boot (via .properties)
📌 Requisito básico

Java 21+

Spring Boot 3.2+

Sem isso, não funciona.

## ✅ Ativação global (HTTP / Web)

No application.properties:

spring.threads.virtual.enabled=true


## 📌 O que isso faz:

O Spring passa a usar Virtual Threads

Cada request HTTP roda em uma Virtual Thread

Substitui o uso de thread pool tradicional do servidor

## 👉 Isso afeta:

Controllers

Filters

Interceptors

Stack inteira da request

## 🧠 O que muda na prática

Antes:

Request → Thread do SO

Pool limitado

Bloqueio caro

Depois:

Request → Virtual Thread

Milhares de requests simultâneos

Bloqueio barato

## ⚠️ O que isso NÃO faz

❌ Não transforma código CPU-bound em rápido
❌ Não paraleliza cálculos
❌ Não muda parallelStream
❌ Não mexe em Fork/Join

## 👉 Só muda como as threads são alocadas

## 🧪 Como verificar se está funcionando
Log simples
@GetMapping("/test")
public String test() {
    System.out.println(Thread.currentThread());
    return "ok";
}


Você verá algo parecido com:

VirtualThread[#23]/runnable@ForkJoinPool-1-worker-1

## 🧵 Virtual Threads fora do HTTP
Executor manual (recomendado)
@Bean
ExecutorService virtualThreadExecutor() {
    return Executors.newVirtualThreadPerTaskExecutor();
}


Uso:

executor.submit(() -> tarefa());

## 🧠 Importante: Banco de dados

Virtual Threads funcionam muito bem com:

JDBC

JPA

Hibernate

## ⚠️ Mas:

O banco ainda tem pool de conexões

Se o pool for pequeno → gargalo continua

## 👉 Virtual Threads ≠ conexões infinitas

## 🚨 Erros comuns

Ativar e achar que tudo escala infinitamente

Esquecer limites do banco

Usar para CPU-bound

Misturar com parallelStream