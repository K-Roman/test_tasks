# Тестовое на позицию стажер DS в KazanExpress

## **Краткое описание задачи**
В наш маркетплейс каждый день поступает множество новых товаров и каждый из них необходимо отнести в определенную категорию в нашем дереве категорий. На это тратится много сил и времени, поэтому мы хотим научиться предсказывать категорию на основе названий и параметров товаров.

# **Описание решения**
Тип данной задачи - иерархическая классифкация. В качестве подхода к решению я выбрал локальный классификатор в каждом узле. То есть сначала я обучаю классифкатор определять родительские категории на верхнем уровне, далее для каждой родительской категории обучаю отдельный классификатор определять дочерние категории и так далее на всю глубину иерархии.

Особенности задачи:

 - разная глубина иерархии для товаров;
 - большой дисбалланс классов. В некоторых родительских категориях множество подкатегорий, в некоторых - всего несколько.

Удалось занять 2-ое место из 50-ти кандидатов, приславших решение. Всего было около 300 кандидатов.

![](https://github.com/K-Roman/test_tasks/blob/main/kazanexpress/leaderboard.JPG)

### **Предобработка текстовых данных**
Текстовые данные из колонок 'title', 'short_description', 'name_value_characteristics' были лемматизириваны, очищены от стоп-слов и знаков препинания. Далее текстовые данные были векторизованы при помощи TF-IDF.

### **Обучение моделей**
В отчете представлены результаты обучения следующих моделей:
 - MultinomialNB;
 - Логистическая регрессия;
 - LinearSVC;
 - RidgeClassifier;
 - DecisionTreeClassifier.
 
### Что сработало:
 - цифры и английские буквы дали небольшой прирост метрики на валидационной выборке, потому что описание некоторых товаров, относящихся к разным категориям, отличаются только названием модели;
 - биграммы.
### Что не сработало:
 - word2vec, нейронные сети(LSTM), предобученный rubert-tiny;
 - включение рейтинга и кол-ва отзывов в обучающую выборку.
### Что можно попробовать:
 - подбор гиперпараметров;
 - проанализировать ошибки, начиная с родительских категорий. Посмотреть какие слова чаще всего встречаются в экземплярах причисленных к неверному классу и попробовать обучить классификатор без этих слов.
