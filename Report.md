**Отчёт о тестировании приложения Money Transfer**

***Краткое описание***

13.11.2020 было проведено тестирование приложения Money Transfer, в ходе которого были выявлены дефекты.
При поступлении на расчетный счет клиента суммы превышающей значение в 2_147_483_647 рублей, новый баланс отображается как отрицательное значение, а при вводе суммы превышающей значение в 2_148_000_000 рублей, отображается ошибка.

***Описание тестов***

Было проведено функциональное тестирование приложения Money Transfer. 
В ходе тестирования проверялся функционал зачисления и отображения денежных средств на расчетном счету.
Для проведения функционального тестирования были использованы эквивалентные значения.
Наименования переменных:
* balance - исходное значение баланса счета;
* transfer_amount - сумма перевода;
* total - переменная для хранения итогового значения.

В качестве тестовых данных использовались следующие эквивалентные значения (в рублях):
1. balance = 0, transfer_amount = 1 - ожидаемый результат: total = 1;
2. balance = 1, transfer_amount = 1_073_741_823 - ожидаемый результат: total = 1_073_741_824;
3. balance = 1_073_741_823, transfer_amount = 1 - ожидаемый результат: total = 1_073_741_824;
4. balance = 0, transfer_amount = 2_147_483_647 - ожидаемый результат: total = 2_147_483_647;
5. balance = 2_147_483_646, transfer_amount = 1 - ожидаемый результат: total = 2_147_483_647;
6. balance = 1, transfer_amount = 2_147_483_645 - ожидаемый результат: total = 2_147_483_647;
7. balance = 2, transfer_amount = 2_147_483_644 - ожидаемый результат: total = 2_147_483_647;
8. balance = 1_073_741_823, transfer_amount = 1_073_741_824 - ожидаемый результат: total = 2_147_483_647;
9. balance = 1_073_741_823, transfer_amount = 1_073_741_828 - ожидаемый результат: total = 2_147_483_651;
10. balance = 455, transfer_amount = 3_000_000_000 - ожидаемый результат: total = 3_000_000_455;
11. balance = 2_000_000_000, transfer_amount = 500_000_000 - ожидаемый результат: total = 2_500_000_000;
12. balance = 456, transfer_amount = 2_800_000_000 - ожидаемый результат: total = 2_800_000_456;
13. balance = 480, transfer_amount = 2_148_000_000 - ожидаемый результат: total = 2_148_000_480;

***Результаты***

61% - успешных тестов, 38% - неуспешных тестов;

Ссылки на баг-репорты:
* [При зачислении на баланс суммы, превышающей значение в 2_147_483_647 рублей, в приложении отображается отрицательный баланс](https://github.com/OlgaNevezhina/MoneyTransfer/issues/1)
* [При зачислении на баланс суммы, превышающей значение в 2_148_000_000 рублей, в приложении отображается ошибка ](https://github.com/OlgaNevezhina/MoneyTransfer/issues/2)

***Общие рекомендации***

В ходе анализа было выявлено, что в коде был использован тип данных int, который имеет диапазон: от -2_147_483_648 до 2_147_483_647. В данном приложении будет уместно использовать тип данных long, так как суммы транзакций в банковском приложении могут превышать 2,2 млрд рублей.
