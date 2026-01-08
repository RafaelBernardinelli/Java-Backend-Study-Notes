
---

## 🧮 `recursive-task.md`

```md
# RecursiveTask<T>

## ❓ Pergunta que responde
👉 Preciso retornar um resultado?

## 💡 O que é
Tarefa recursiva que retorna um valor.

## 🎯 Quando usar
- Soma
- Busca
- Agregações

## ⚠️ Armadilhas

Granularidade errada

Fork excessivo

## 🧪 Exemplo
```java
class SumTask extends RecursiveTask<Integer> {

    protected Integer compute() {
        if (smallEnough()) {
            return computeDirectly();
        }
        SumTask left = new SumTask();
        SumTask right = new SumTask();
        left.fork();
        return right.compute() + left.join();
    }
}
