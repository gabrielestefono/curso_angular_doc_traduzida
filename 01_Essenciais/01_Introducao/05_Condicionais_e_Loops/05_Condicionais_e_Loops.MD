# Condicionais e Loops

Condicionalmente mostram e/ou repetem o conteúdo baseado em dados dinâmicos.

Uma das vantagens de usar frameworks como o Angular é que eles provém soluções simples para problemas comuns que desenvolvedores encontram. Por exemplo, mostrar dados baseado em condições, mostrar uma lista de elementos baseado em dados dinâmicos, etc.

Para resolver esses problemas, Angular usa blocos prontos para dizer ao framework quando e como os templates devem ser mostrados.

## Renderização Condicional

Um dos problemas mais comuns que desenvolvedores encontram é o de mostrar ou esconder dados na tela baseado em condições.

Um dos exemplos disso é se deve ou não mostrar alguns dados baseados no nível de permissão do usuário.

## bloco @if

Similar ao if do javascript, Angular usa o controlador `@if` para mostrar ou esconder condicionalmente partes do template e seu conteúdo.

```js
// user-controls.component.ts
@Component({
  standalone: true,
  selector: 'user-controls',
  template: `
    @if (isAdmin) {
      <button>Erase database</button>
    }
  `,
})
export class UserControls {
  isAdmin = true;
}
```

Neste exemplo, Angular só irá renderizar o botão se a propriedade admin for true. Em outro caso, o botão não aparece na página.

## bloco @else

Enquanto o bloco `@if` pode ser muito útil em várias situações, é comum mostrar um template alternativo quando a condição não é atendida.

Por exemplo, no componente `UserControl`, ao invés de uma tela branca, pode ser útil ao usuário que ele saiba que ele não pode ver nada por não estar autenticado.

Quando você precisa de um fallback, similar ao else do javascript, adicione um bloco `@else` para o mesmo efeito.

```js
// user-controls.component.ts
@Component({
  standalone: true,
  selector: 'user-controls',
  template: `
    @if (isAdmin) {
      <button>Erase database</button>
    } @else {
      <p>You are not authorized.</p>
    }
  `,
})
export class UserControls {
  isAdmin = true;
}
```

## Renderizando uma lista

Similar aos loops `for...of` o Angular te dá o bloco `@for` para renderizar elementos repetidos.

```jsx
<!-- ingredient-list.component.html -->
<ul>
  @for (ingredient of ingredientList; track ingredient.name) {
    <li>{{ ingredient.quantity }} - {{ ingredient.name }}</li>
  }
</ul>
```

```js
// ingredient-list.component.ts
@Component({
  standalone: true,
  selector: 'ingredient-list',
  templateUrl: './ingredient-list.component.html',
})
export class IngredientList {
  ingredientList = [
    {name: 'noodles', quantity: 1},
    {name: 'miso broth', quantity: 1},
    {name: 'egg', quantity: 2},
  ];
}
```

No entando, diferente do loop `for...of`, você deve ter notado que existe a palavra chave `track` adicional.

## Propriedade track

Quando o Angular renderiza uma lista de elementos com `@for`, esses itens podem posteriormente mudar ou se mover. O Angular precisa acompanhar cada elemento através de qualquer reordenação, geralmente tratando uma propriedade do item como um identificador único ou chave.

Isso garante que quaisquer atualizações na lista sejam refletidas corretamente na interface do usuário e rastreadas adequadamente dentro do Angular, especialmente no caso de elementos com estado ou animações.

Para realizar isso, podemos fornecer uma chave única ao Angular com a palavra-chave `track`.