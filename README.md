# game-server

Игра Домино на трёх человек.

Содержит в себе сервер HTTP для выдачи статики, и WebSocket для поддержания соединения с игроками.

## Запуск

Устанавливаем зависимости:
```
npm i
```

Запускаем сборку:
```
npm run build
```

Запускаем сервер:
```
npm start
```

## Подключение игроков

В браузере открываем http://localhost:8000/

Игра запускается на трёх игроков. Сервер последовательно соединяет трёх подключившихся клиентов в игру.

## Начало игры

Начинает тот игрок, у которого есть кость с дублем 6-6, он выставляет её. Если же ни у кого из игроков нет дубля 6-6, то можно ходить другими дублями, например 5-5, 4-4 и т.д. от большего к меньшему. А если ни у кого нет дубля, то ходят костью с наибольшей суммой значений, начиная от 6-5 и т.д.

## Игровой процесс

Каждый по кругу выкладывает кость, одно из значений которой совпадает со значением на одном из концов цепи, тем самым продолжая цепь (когда костяшка одна, концы - её пара значений, когда две - свободные значения, т.е. те, которые не участвуют в их связи и т.д.). Если игроку нечего выложить, он добирает кости из базара до тех пор, пока не попадётся подходящая, после чего он выкладывает её. Пропускать ход можно только тогда, когда выложить нечего, а базар пуст.

## Игровой интерфейс

Текущий игрок выбирает костяшку и последовательно пару соседних клеток (у костяшек первое значение — левое, второе — правое). Порядок неважен: можно выбрать сначала либо клетки, либо костяшку. Если пользователю нечем ходить, он может нажать кнопку сверху "Take from Bazaar". Если после постановки костяшки на поле пользователь может нажать кнопку справа сверху "Cancel". Для завершения хода (либо его пропуска) пользователь должен нажать кнопку справа сверху "End turn".
Перемещать область видимости можно с помощью колесика мыши (если зажат Alt — область перемещается по горизонтали) или стрелками на клавиатуре.

## Окончание игры

Партия кончается тогда, когда один из игроков выложит свою последнюю костяшку. Победителю записывается сумма очков со всех костяшек у проигравших.
Партия может закончиться когда кости на руках будут, но нечего будет докладывать. В этой ситуации выигрыш принадлежит тому, у кого меньше всего очков. В выигрыш ему записывается разность очков между суммой очков со всех костяшек у проигравших и суммой его очков (для такого исхода необходимо, чтобы все игроки по очереди пропустили свой ход)