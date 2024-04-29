# Renderizando Templates Dinamicos

Use templates Angular para criar HTML dinâmico.

O que você aprendeu até agora, deixa você quebrar uma aplicação em componentes HTML, mas isso te limita a templates estáticos. O próximo passo é aprender como usar os templates dinâmicos do Angular para criar HTML dinâmico.

## Renderizando dados dinâmicos.

Quando você precisa mostrar dados dinâmicos no seu template, no angular, você usa as chaves duplas para destinguir dados dinâmicos de dados estáticos, 

Aqui um exemplo simplificado de um componente ToDoListItem:

```js
@Component({
  selector: 'todo-list-item',
  template: `
    <p>Title: {{ taskTitle }}</p>
  `,
})
export class TodoListItem {
  taskTitle = 'Read cup of coffee';
}
```

Quando o Angular renderizar o componente, você verá o output:

```html
<p>Title: Read cup of coffee</p>
```

Essa sintaxe declara uma interpolação entre os dados dinâmicos dentro do HTML. Como resultado, sempre que os dados mudarem, o angular mudará automaticamente o DOM refletindo o valor das propriedades.

## Propriedades dinâmicas

Quando você precisa setar dinamicamente o valor do DOM padrão em um HTML, a propriedade é colocada entre colchetes para informar ao Angular que o valor deve ser interpretado como um elemento JavaScript ao invés de string pura.

Um exemplo comum de setar dinamicamente propriedades no seu HTML é determinando quando um botão de formulário deve ser desabilitado baseado em, se o formulário é válido ou não.

Coloque a propriedades em colchetes para dizer ao Angular que o valor é dinâmico e não estático.

```js
@Component({
  selector: 'sign-up-form',
  template: `
    <button type="submit" [disabled]="formIsInvalid">Submit</button>
  `,
})
export class SignUpForm {
  formIsInvalid = true;
}
```

neste exemplo, pelo formIsInvalid ser true, o valor renderizado no HTML deve ser de:
```html
<button type="submit" disabled>Submit</button>
```

## Atributos dinâmicos

Caso você queira vincular dinamicamente atributos HTML personalizados (por exemplo, aria-, data-, etc.), você pode pensar em agrupar os atributos personalizados com os colchetes.

```js
@Component({
  standalone: true,
  template: `
    <button [data-test-id]="testId">Primary CTA</button>
  `,
})
export class AppBanner {
  testId = 'main-cta';
}
```

Infelizmente, isso não funcionará, porque os atributos não são propriedades padrões do DOM. Ao invés disso, para que isso funcione como esperado, devemos adicionar aos atributos HTML personalizados o prefixo `attr.`

```js
@Component({
  standalone: true,
  template: `
    <button [attr.data-test-id]="testId">Primary CTA</button>
  `,
})
export class AppBanner {
  testId = 'main-cta';
}
```
