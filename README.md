# colorization
## Основная идея
Цель работы заключается в реализации глубокой нейронной сеть для окраски черно-белых изображений. Для достижения поставленной цели был использован готовый набор данных, содержащий в себе порядка семи тысяч изображений неодинаковых размеров и разрешений. В него входят картинки, на которых представлены люди, собаки, кошки, цветы, мотоциклы, самолёты, фрукты и автомобили. 
## Реализация
Для достижения цели была реализована модель логистической регрессии. В данной работе используется цветовая палитра модели CIELAB. Она комбинирует 3 численных значения: канал светлости (lightness, шкала от 0 до 100), канал A (содержит позиции цветов от зелёного до пурпурного и лежит в диапазоне [-128; 128]), канал B (цвета от синего до желтого в промежутке [-128; 128]).
Перед подачей набора данных в сеть, они проходят предобработку. Она включает в себя перевод изображений в черно-белый формат, который оставляет один канал светлоты (L), и нормализацию по вем образцам выборки (она производилась относительно среднего значения по каждому каналу L, A, B по всем образцам выборки. ).
Во втором фрагменте модели глубина картинки растет и последовательно доходит до 512. Слой за слоем исходное значение пикселей переходят в оценку классов.  Образцы размером 256х256х512 уже выходят из сети и подвергаются следующим преобразованиям. Каждое изображение из батча делиться на 2 части (глубина каждого равна 256). Одна часть нужна для классификации пикселей для канала A, вторая – для B.
Далее у каждого пикселя в каждой части большого тензора находится наиболее вероятный класс, для которого сеть выдала наиболее уверенный ответ. Это получается последовательным применением методов Softmax и argmax.
Для обучения сети был использован алгоритм кросс-энтропийной потери.
## Результаты
На маленькой выборке:
![image](https://user-images.githubusercontent.com/48317053/94053172-6a44de80-fdf3-11ea-890e-f4ff2f3ed7fc.png)
На большой выборке:
