
---

## 🧮 `recursive-action.md`

```md
# RecursiveAction

## ❓ Pergunta que responde
👉 Não preciso retornar resultado?

## 💡 O que é
Versão do Fork/Join sem retorno.

## 🎯 Quando usar
- Mutação de estruturas
- Processamento in-place

## ⚠️ Armadilhas

Efeitos colaterais concorrentes

## 🧪 Exemplo
```java
class ActionTask extends RecursiveAction {

    protected void compute() {
        if (smallEnough()) {
            work();
        } else {
            invokeAll(new ActionTask(), new ActionTask());
        }
    }
}
