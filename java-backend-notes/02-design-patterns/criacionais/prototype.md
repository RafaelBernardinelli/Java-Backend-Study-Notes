
---

# 🧩 Exemplo real — `prototype.md`

```md
# Prototype Pattern

## 💡 O que é
Define criação de **novas instâncias** a cada solicitação (no Spring, `@Scope("prototype")`).

## 🎯 Quando usar
- Objetos com estado temporário por operação.
- Geradores de relatório, builders mutáveis por requisição.

## ❌ Quando NÃO usar
- Beans que devem ser singletons (services sem estado).
- Injetar protótipos diretamente em singletons sem cuidado.

## 🧠 Relação com SOLID / DI
- DIP continua válido; atenção ao ciclo de vida.
- SRP: prototype pode conter estado por operação.

## ⚠️ Armadilhas comuns

Injetar prototype diretamente em singleton (mesma instância usada) — use ObjectProvider ou Provider.

## ✅ Checklist arquitetural

 Uso de provider para obter novas instâncias?

 Prototype limpo após uso?

 Testes que verificam nova instância por chamada?

## 🧪 Como testar rápido

Chamar provider.getObject() duas vezes e checar !=.

## 🧪 Exemplo em Java + Spring
```java
@Component
@Scope("prototype")
public class ReportGenerator {
    private final List<String> lines = new ArrayList<>();
    public void add(String line) { lines.add(line); }
    public String generate() { return String.join("\n", lines); }
}

@Service
public class ReportService {
    private final ObjectProvider<ReportGenerator> provider;
    public void createReport() {
        ReportGenerator g = provider.getObject();
        g.add("linha");
        g.generate();
    }
}
