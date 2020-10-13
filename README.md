<H1>Задачи классификации
<H2>Метрические алгоритмы классификации
  
Мы будем рассматривать такие алгоритмы классификации, как:
- kNN - k Nearst Neighbor
- 1NN - частный случай kNN
- kwNN

Начнём с того, что наши алгоритмы мы будем испытывать с помощью датасета "Ирисы Фишера", а именно выборка по ширине, длине лепестка, а также виду ириса.

Наглядное изображение нашей выборки:
![screenshot of sample](https://github.com/KlochkovVLAD/lab1/blob/main/Iris.png)

Для классификации точек будем использовать обычную евклидову метрику

И так, начнём

Первым у нас идёт алгоритм 1NN, который заключается в том, чтобы найти в нашей выборке точку, которая находится ближе всего к заданной. Далее просто присваиваем нашей точке тот же самый класс.

Карта классификации для 1NN:
![screenshot of sample](https://github.com/KlochkovVLAD/lab1/blob/main/1NN.jpg)

Далее рассмотрим алгоритм kNN:
- Находим расстояния от нашей точки до всех точек выборки
- Сортируем все расстояния по возрастанию
- Берём первые k точек и находим среди них класс, который встречается чаще всего и присваиваем его нашей точке

В данном алгоритме возникает проблема нахождения оптимального значения k, при котором вероятность ошибки будет минимальной.
Для этого нам необходим ещё один алгоритм - LOO

Алгоритм LOO:
- Берём нашу выборку
- Для каждой точки нашей выборки используем алгоритм kNN, перебирая все значения k
- Записываем количество ошибок для каждого значения k
- Берём k с минимальным количеством ошибок

Для нашего случая оптимальным оказалось k=6 

Карта классификация для kNN, при k=6:
![screenshot of sample](https://github.com/KlochkovVLAD/lab1/blob/main/kNN.jpg)

Следующий по списку, но не по качеству - алгоритм kwNN, смысл которого дать каждой точке её вес относительно нашей точки и определить класс, который "весит" больше всего, просуммировав все веса точек данного класса.

Алгоритм kwNN:
- Находим расстояния от нашей точки до всех точек выборки
- Сортируем все расстояния по возрастанию
- Берём k точек и присваиваем им вес по формуле q^i, где i номер точки по удалению относительно нашей
- Суммируем все веса одинаковых классов
- Присваиваем нашей точке класс с максимальной суммой весов

Откуда брать k и q, оба значения находим по алгоритму LOOQ, оптимальное k у нас есть из kNN, остаётся найти оптимальное q.

Алгоритм LOOQ:
- Берём нашу выборку
- Для каждой точки нашей выборки используем алгоритм kwNN, перебирая все значения q
- Записываем количество ошибок для каждого значения q
- Берём q с минимальным количеством ошибок

Карта классификации для kwNN, при k=6, q=0.56:
![screenshot of sample](https://github.com/KlochkovVLAD/lab1/blob/main/kwNN.png)

Вероятности ошибок каждого из алгоритмов на данной выборке:
![screenshot of sample](https://github.com/KlochkovVLAD/lab1/blob/main/tableOfErrors.png)

На данной выборке алгоритм kwNN показал себя хуже, чем kNN, но если взять выборку, в которой точки будут расположены плотнее, а расстояния между разными классами меньше, то алгоритм kwNN покажет лучший результат (это мои субъективные выводы).

Примеры всех кодов можно посмотреть в репозитории.
