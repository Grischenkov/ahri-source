# Last.fm-artist-recommender-pipeline

**Автор**: *Грищенков Н. Д., Р4140*

## Цель

Разработать систему для поиска похожих музыкальных исполнителей.

## Задачи

1. Проанализировать датасет.
2. Спроектировать архитектуру системы.
3. Подготовить данные для обучения и тестирования моделей.
4. Обучить модели.
5. Получить оценки моделей.
6. Выбрать оптимальную модель.
7. Выполнить развертывание наилучшей модели.

## EDA

+ Данные об исполнителях:
    + Имеем информацию о 17493 исполнителях.
    + Столбцы:
        + artist_id
        + artist_name
    + Пропуски в данных отсутствуют.
    + Есть одно повторяющееся имя исполнителя с разными id. 
    Удалять не будем, так как может существовать несколько исполнителей с одним названием.

+ Данные о прослушиваниях
    + Имеем 92723 записей.
    + Столбцы:
        + user_id
        + artist_id
        + scrobbles (число прослушиваний)
    + Пропуски в данных отсутствуют.
    + Есть повторяющиеся пары id пользователя и исполнителя с разным числом прослушиваний.
    Возможные варианты обработки:
        + <u>Удалить дубликаты</u>
        + Суммировать число прослушиваний
        + Усреднить значения прослушиваний
    + Большая часть пользователей имеет информацию о прослушивании 50 исполнителей, однако есть пользователи, прослушавшие меньшее количество, в том числе всего одного исполнителя.
    Удалять таких пользователей из выборки не следует, так как в этом случае информация о прослушиваниях будет не для всех исполнителей.

## Оценка качества
При оценке качества будем отталкиваться от гипотезы о том, что пользователи слушают схожих исполнителей или несколько групп схожих исполнителей.

Пользователь прослушал n исполнителей. Тогда мы можем для каждого исполнителя, прослушанного пользователем, порекомендовать k похожих исполнителей, составить список из k*n рекомендаций пользователю и рассчитать количество совпадений. Затем поделить его на число рекомендаций.

Итоговая оценка качества для всех пользователей: среднее оценок для каждого пользователя.

При оценке не будем учитывать пользователей, прослушавших только одного исполнителя, так как для них невозможно корректно получить такую оценку.

## Deploy diagram

 ![Deploy diagram](img/deploy_diagram.png?raw=true "Deploy diagram")

## Workflow diagram

 ![Workflow diagram](img/workflow_diagram.png?raw=true "Workflow diagram")

## Ссылки

1. [Датасет](https://www.kaggle.com/datasets/pcbreviglieri/lastfm-music-artist-scrobbles)
2. [Репозиторий](https://github.com/Grischenkov/Last.fm-artist-recommender-pipeline)