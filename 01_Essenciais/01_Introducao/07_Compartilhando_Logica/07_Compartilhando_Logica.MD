# Compartilhando Logica

Injeção de dependências te permite compartilhar o código.

Quando você precisa compartilhar lógica entre os componentes, Angular alavanca o padrão de design de injeção de dependências, que te permite criar um service, que te permite injetar código dentro de componentes enquanto gerencia ele de uma só fonte de verdade.

## O que são serviços?

Serviços são pedaços reutilizáveis de código que podem ser injetados.

Similarmente à definição de componentes, serviços são compostos por:
* Um decorator typescript que declara a classe Service Angular pelo decorator `@Injectable` e te permite definir qual parte da aplicação pode acessá-lo pela propriedade `providedIn` (que normalmente é `root`), que permite que o service possa ser acessado em qualquer lugar dentro da aplicação.
* Uma classe typescript que define o código que será acessível quando o serviço for injetado.

Aqui um exemplo de um serviço de uma calculadora:
```js
import {Injectable} from '@angular/core';
@Injectable({
  providedIn: 'root',
})
export class CalculatorService {
  add(x: number, y: number) {
    return x + y;
  }
}
```

## Como usar um service

Quando você quiser usar um componente service, você precisa:

1. Importar o service
2. Declare um campo de classe onde o serviço é injetado. Atribua o campo de classe ao resultado da chamada da função interna inject que cria o serviço

Aqui como o código deve parecer no componente `Receptor`:

```js
import { Component } from '@angular/core';
import { CalculatorService } from './calculator.service';
@Component({
  selector: 'app-receipt',
  template: `<h1>The total is {{ totalCost }}</h1>`,
})
export class Receipt {
  private calculatorService = inject(CalculatorService);
  totalCost = this.calculatorService.add(50, 25);
}
```

neste exemplo, o service da Calculadora está sendo usado/chamado por chamar a função `inject` e passando dentro dele o service para a função.