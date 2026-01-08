
---

## 🧾 `copy-on-write-arraylist.md`

```md
# CopyOnWriteArrayList

## ❓ Pergunta que responde
👉 Muitas leituras e poucas escritas?

## 💡 O que é
Lista que cria **uma cópia inteira** a cada modificação.

Leitura é extremamente rápida e sem lock.

## 🎯 Quando usar
- Configurações
- Observers
- Listas quase imutáveis

## ❌ Quando NÃO usar

Muitas escritas

Listas grandes

## ⚠️ Armadilhas

Alto custo de escrita

Iteradores não veem mudanças recentes

## ✅ Checklist

 Escritas raras?

 Tamanho controlado?

## 🧪 Exemplo
```java
List<String> list = new CopyOnWriteArrayList<>();

list.add("A");
list.forEach(System.out::println);
