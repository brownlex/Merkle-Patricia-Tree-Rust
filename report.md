В начале разработки я воспользовался материалами, описывающими данную структуру:
https://en.wikipedia.org/wiki/Radix_tree <br />
https://en.wikipedia.org/wiki/Merkle_tree <br />
https://github.com/ethereum/wiki/wiki/Patricia-Tree
http://general-beck.info/ethereum-%D1%8D%D1%84%D0%B8%D1%80%D0%B8%D1%83%D0%BC/664-%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D1%8C%D1%8F-%D0%BC%D0%B5%D1%80%D0%BA%D0%BB%D0%B0-%D0%B2-%D1%8D%D1%84%D0%B8%D1%80%D0%B8%D1%83%D0%BC%D0%B5 <br />

Так же использовал для изучения реализацию структуры от Ethereum:
https://github.com/ethereumjs/merkle-patricia-tree

## Краткое описание структур:
+ Radix Tree (aka Prefix Tree)  -- упорядоченное дерево, которое используется для хранения динамичного набора данных или ассоциативного массива, где ключи, как правило, -- строки. <br />
+ Merkle Tree -- такое дерево, в котором каждый узел без листьев содержит хеш его дочерних узлов (в случае листьев -- хеш значений) <br />

# Процесс разработки

### В ходе работы мне понадобились следующие библиотеки

rust serialize - для сериализации данных
bincode - компактный энкодер/декодер, использующий бинарную схему кодирования
crypto - для хеширования данных

Я создал trait, в котором описал доступные пользователю функции для работы с деревом (создать новое,
вставить, взять, удалить), а остальные, связаные с сжатием и хешированием, реализвал с помощью отдельного impl (на мой взгляд, это увеличивает читабельность и так проще ориентироваться в коде)

### Плюсы реализации

+ Дерево корректно выполняет свою работу
+ Интуитивно понятный интерфейс
+ Достаточно читабельный код

### Минусы реализации

- Не удалось в полной мере использовать заимствование
- При достаточно больших значениях функция вставки выполняется достаточно долго