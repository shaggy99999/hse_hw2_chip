# hse_hw2_chip

Цель этого практического задания - определить участки генома, где присутствует определенная гистоновая модификация в конкретном типе клеток с помощью анализа ChIP-Seq данных. 


Выбранный образец: 
1. клеточная линия: HeLa-S3	
2. Гистоновая метка: H3K4me3	
3. Реплика 1:ENCFF001FLG и Реплика 2: ENCFF001FLD	(ссылка https://www.encodeproject.org/experiments/ENCSR000DUA/)
4. Контроль: ENCFF001HNS (ссылка https://www.encodeproject.org/experiments/ENCSR000DTX/)

Ссылка на колаб:  https://colab.research.google.com/drive/1YMGGqUXh61EeqcmM9m9oUDH5X563qU3X?usp=sharing

## 1. Анализ Fastq

Для того, чтобы правильно подгтотвить файлы и выяснить, нужно ли их обрабатывать дополнительно, посмотрим на отчет fastqc.

 1) ENCFF001FLG

Исходя из отчета fastqc, я бы сказала, что нужно дополнительно обрабатывать чтения. Рассмотрим подробнее некоторые ключевые графики.

Несмотря на то, что Per Tile Sequence Quality отмечен как непрошедший проверку качества график, основное полотно синего цвета, который свидетельствует о хорошем качестве для tiles, посмотрим какой будет результат после подрезаний чтений:

до подрезания чтений:
<p float="left">
  <img src="/image/1.png" width="400" />
  <img src="/image/2.png" width="400" />
  <img src="/image/3.png" width="400" />
  <img src="/image/4.png" width="400" />
</p>

Для первой реплики ENCFF001FLG подрезания чтений улучшили картину.

после подрезания чтений:
<p float="left">
  <img src="/image/5.png" width="400" />
  <img src="/image/6.png" width="400" />
  <img src="/image/7.png" width="400" />
  <img src="/image/8.png" width="400" />
</p>

 2) ENCFF001FLD

После был проанализирован fastqc для ENCFF001FLD. Ситуация аналогична первого пункту и подрезания чтений совсем немного улучшает качество Per Tile Sequence Quality.

до:
<p float="left">
  <img src="/image/9.png" width="400" />
  <img src="/image/10.png" width="400" />
  <img src="/image/11.png" width="400" />
  <img src="/image/12.png" width="400" />
</p>

после:
<p float="left">
  <img src="/image/13.png" width="400" />
  <img src="/image/14.png" width="400" />
  <img src="/image/15.png" width="400" />
  <img src="/image/16.png" width="400" />
</p>

Для файла контроля ENCFF001HNS также подрезали чтения(в принципе можно было не делать, тк для контроля отчет изначально был лучше, чем для реплик):

до:
<p float="left">
  <img src="/image/17.png" width="400" />
  <img src="/image/18.png" width="400" />
  <img src="/image/19.png" width="400" />
  <img src="/image/20.png" width="400" />
</p>

после:
<p float="left">
  <img src="/image/21.png" width="400" />
  <img src="/image/22.png" width="400" />
  <img src="/image/23.png" width="400" />
  <img src="/image/24.png" width="400" />
</p>

Вывод: качество образцов допустимо для дальнейшей обработки
## Выравнивание на хромосому

Таблица со статистикой по каждому из 3 образцов:
|                        |      total reads |   aligned 0 times | aligned exactly 1 time| aligned >1 times |
|------------------------|------------------|-------------------|-----------------------|------------------|
|ENCFF001FLG (реплика 1) |   30895722       | 28027119 (90.72%) | 1174449 (3.80%)       | 1694154 (5.48%)  |
|ENCFF001FLD (реплика 2) |   14724307       | 12642731 (85.86%) | 804266 (5.46%)        | 1277310 (8.67%)  |
|ENCFF001HNS (контроль)  |   18602597       | 14838049 (79.76%) | 1070793 (5.76%)       | 2693755 (14.48%) |
 

```
Q: Почему процент выравниваний получился именно таким?
A:
```

## Cравнение результатов

Диаграммы Венна:


<p float="left">
  <img src="/image/v1.png" width="400" />
  <img src="/image/v2.png" width="400" />
</p>

```
Q: Как можно объяснить различия в количестве пересечений?
A: Пересечений получилось мало, потому что и наших пиков получилось мало в силу того, что выравнивание было произведено только на одну хромосому. В базе данных ENCODE же пики составлены для всех хромосом, поэтому их число намного больше. Касаемо того, почему пересечение наших пиков с пиками ENCODE и пересечение пиков ENCODE с нашими пиками - это не одно и то же: все потому, что пересечение устроено таким образом, что считается число участков в первом файле таких, что они также имеются и во втором. Таким образом понятно, почему при перемене файлов местами мы получаем разный результат.
```
