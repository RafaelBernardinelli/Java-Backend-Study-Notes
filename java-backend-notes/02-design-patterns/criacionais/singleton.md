# Singleton Pattern

## 💡 O que é
Garante que haja **uma única instância** de uma classe por `ApplicationContext` (ou JVM, dependendo da implementação).

## 🎯 Quando usar
- Componentes compartilhados sem estado (services, repositories).
- Recursos caros de criar, que precisam ser únicos.

## ❌ Quando NÃO usar
- Objetos com estado por requisição/usuário.
- Contadores/coleções mutáveis sem sincronização.

## 🧠 Relação com SOLID / DI
- DIP: o cliente depende de abstração, o container fornece a instância.
- SRP: singleton é apenas uma escolha de escopo, não de responsabilidade.

## ⚠️ Armadilhas comuns

Aderir estado mutável em campos de instância.

Assumir thread-safety sem sincronização.

## ✅ Checklist arquitetural

- Bean é stateless?

- Injeção por construtor?

- Nenhum atributo mutável compartilhado?

## 🧪 Como testar rápido

- Criar dois beans que recebam o mesmo UserService e verificar ==.

## 🧪 Exemplo em Java + Spring
```java
@Service // por padrão singleton
public class UserService {
    public User findById(Long id) { ... }
}
