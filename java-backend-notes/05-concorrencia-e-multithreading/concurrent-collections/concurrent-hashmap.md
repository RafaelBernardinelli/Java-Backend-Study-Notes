# ConcurrentHashMap

## ❓ Pergunta que responde
👉 Várias threads lendo e escrevendo ao mesmo tempo?

## 💡 O que é
Mapa concorrente de alta performance.
Permite múltiplas leituras e escritas simultâneas.

Diferente do `HashMap`, **não trava o mapa inteiro**.

## 🎯 Quando usar
- Cache
- Contadores
- Mapas compartilhados
- Estados globais concorrentes

## ❌ Quando NÃO usar

Quando precisa de ordenação

Quando mutações são raras

## ⚠️ Armadilhas

size() não é exato em tempo real

Operações compostas precisam compute

## ✅ Checklist

 Uso de compute?

 Evitou sincronização externa?

## 🧪 Exemplo
```java
Map<String, Integer> map = new ConcurrentHashMap<>();

map.put("a", 1);
map.compute("a", (k, v) -> v + 1);
