# Gerenciando Dados Dinamicos

Define o estado e o comportamento para gerenciar dados dinâmicos.

Agora que nós aprendemos a estrutura básica para um componente, vamos começar a aprender como você pode definir dados no componente, estado e comportamento.

## O que é um estado?

Componentes permitem que você encapsule de forma organizada a responsabilidade por partes discretas de sua aplicação. Por exemplo, um componente SignUpForm pode precisar manter o controle sobre se o formulário é válido ou não antes de permitir que os usuários realizem uma ação específica. Como resultado, as várias propriedades que um componente precisa rastrear são frequentemente referidas como "estado".

## Definindo estado.

Para definir um estado, você usa atributos de uma classe dentro de seu componente.

1. taskTitle = Qual é o título da sua task.
2. isComplete = A tarefa está ou não concluída.

```js
// todo-list-item.component.ts
@Component({ ... })
export class TodoListItem {
  taskTitle = '';
  isComplete = false;
}
```

## Atualizando Estado.

Quando você quer atualizar um estado, isso normalmente é feito definindo métodos na classe do componente, ele pode acessar os vários atributos com a palavra `this`.

```js
// todo-list-item.component.ts
@Component({ ... })
export class TodoListItem {
  taskTitle = '';
  isComplete = false;
  completeTask() {
    this.isComplete = true;
  }
  updateTitle(newTitle: string) {
    this.taskTitle = newTitle;
  }
}
```
