# debounce

Выдаёт значение из источника Observable только после того как пройдёт некоторый промежуток времени.

## Сигнатура

```typescript
debounce<T>(durationSelector: (value: T) => SubscribableOrPromise<any>): MonoTypeOperatorFunction<T>
```

## Описание

Это похоже на `debounceTime`, но промежуток времени определяется `next`-ом внешнего потока.
`debounce` задерживает значение, высвобождаемое источником Observable, но снижает предыдущие отложенные выделения, если в источник Observable поступает новое значение. Этот оператор следит за последним значением из источника Observable и генерирует длительность Observable, вызывая функцию `durationSelector`. Значение выдается только тогда, когда длительность Observable выдаёт значение или завершается, и если из источника Observable не было выдано другое значение с момента появления длительности Observable. Если до истечения срока действия функции Observable появляется новое значение, то предыдущее значение будет сброшено и не будет выдано в результате Observable.
Как и в случае с `debounceTime`, это оператор с ограничением скорости, а также оператор с возможной задержкой, так как на выходе выделения не обязательно происходят в то же самое время, что и на источнике Observable.

## Параметры

| Название | Описание |
|-|-|
| durationSelector | Функция, которая получает значение из источника Observable для вычисления продолжительности таймаута для каждого значения источника, возвращаемого в качестве Observable или Promise. |

## Примеры

Произвести последний клик после серии кликов.

```typescript
import { fromEvent, interval } from 'rxjs';
import { debounce } from 'rxjs/operators';

const clicks = fromEvent(document, 'click');
const result = clicks.pipe(debounce(() => interval(1000)));
result.subscribe(x => console.log(x));
```

## Полезные ссылки

- 📰 Официальная документация: [debounce](https://rxjs.dev/api/operators/debounce)
- 📁 Исходный код: https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/pipeable/debounce.ts
