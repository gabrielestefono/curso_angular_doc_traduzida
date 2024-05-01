# Lidando com Interacao do Usuário

Lide com a interação do usuário na sua aplicação.

A habilidade de lidar com a interação do usuário e então trabalhar com ela - é um dos aspectos de criação de aplicações dinâmicas. Nesse guia, vamos ver um pouco sobre lidar com interação do usuário - Manipuladores de eventos.


## Manipuladores de Eventos

Você pode adicionar um novo manipulador de eventos da seguinte forma:

1. Adicionando um atributo com o nome do evento entre parênteses
2. Especifique qual instrução Javascript você quer que execute quando for chamado.

```html
<button (click)="save()">Save</button>
```

Por exemplo, se nós quisermos criar um botão que vai rodar uma função chamada transformText quando o evento click for executado, isso deve ficar assim:

```js
// text-transformer.component.ts
@Component({
  standalone: true,
  selector: 'text-transformer',
  template: `
    <p>{{ announcement }}</p>
    <button (click)="transformText()">Abracadabra!</button>
  `,
})
export class TextTransformer {
  announcement = 'Hello again Angular!';
  transformText() {
    this.announcement = this.announcement.toUpperCase();
  }
}
```

Outros exemplos comuns de eventos incluem:

```html
<input (keyup)="validateInput()" />
```

```html
<input (keydown)="updateInput()" />
```

## $event

Se você precisa acessar o objeto de evento, o Angular te dá uma variável `$event`, que você pode passar para a função:

```html
<button (click)="createUser($event)">Submit</button>
```