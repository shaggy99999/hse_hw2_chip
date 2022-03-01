# hse_hw2_chip

Цель этого практического задания - определить участки генома, где присутствует определенная гистоновая модификация в конкретном типе клеток с помощью анализа ChIP-Seq данных. 


Выбранный образец: 
1. клеточная линия: HeLa-S3	
2. Гистоновая метка: H3K4me3	
3. Реплика 1:ENCFF001FLG и Реплика 2: ENCFF001FLD	(ссылка https://www.encodeproject.org/experiments/ENCSR000DUA/)
4. Контроль: ENCFF001HNS (ссылка https://www.encodeproject.org/experiments/ENCSR000DTX/)

Ссылка на колаб:  https://colab.research.google.com/drive/1YMGGqUXh61EeqcmM9m9oUDH5X563qU3X?usp=sharing

## 1. Анализ Fastq

Для первой реплики ENCFF001FLG подрезания чтений улучшили картину.:

до подрезания чтений:

<p float="left">
  <img src="/image/1.png" width="300" />
  <img src="/image/2.png" width="300" />
  <img src="/image/3.png" width="300" />
  <img src="/image/4.png" width="300" />
</p>

после подрезания чтений:

<p float="left">
  <img src="/image/5.png" width="250" />
  <img src="/image/6.png" width="250" />
  <img src="/image/7.png" width="250" />
  <img src="/image/8.png" width="250" />
</p>

После был сделан fastqc для ENCFF001FLD

Очевидно, что подрезания улучшили картину.

до:

<p float="left">
  <img src="/pictures/9.png" width="250" />
  <img src="/pictures/10.png" width="250" />
  <img src="/pictures/11.png" width="250" />
  <img src="/pictures/12.png" width="250" />
</p>

после:

<p float="left">
  <img src="/pictures/13.png" width="250" />
  <img src="/pictures/14.png" width="250" />
  <img src="/pictures/15.png" width="250" />
  <img src="/pictures/16.png" width="250" />
</p>

Для файла контроля ENCFF001HNS также подрезали чтения(в принципе можно было не делать):
до:
<p float="left">
  <img src="/pictures/17.png" width="250" />
  <img src="/pictures/18.png" width="250" />
  <img src="/pictures/19.png" width="250" />
  <img src="/pictures/20.png" width="250" />
</p>
после:
<p float="left">
  <img src="/pictures/21.png" width="250" />
  <img src="/pictures/22.png" width="250" />
  <img src="/pictures/23.png" width="250" />
  <img src="/pictures/24.png" width="250" />
</p>
## Выравнивание на хромосому

Таблица со статистикой по каждому из 3 образцов:
|                        |      total reads |   aligned 0 times | aligned exactly 1 time| aligned >1 times |
|------------------------|------------------|-------------------|-----------------------|------------------|
|ENCFF001FLG (реплика 1) |   30895722       | 28027119 (90.72%) | 1174449 (3.80%)       | 1694154 (5.48%)  |
|ENCFF001FLD (реплика 2) |   14724307       | 12642731 (85.86%) | 804266 (5.46%)        | 1277310 (8.67%)  |
|ENCFF001HNS (контроль)  |                  |                   |                       |                  |
 

```
Q: Почему процент выравниваний получился именно таким?
A:
```

## Cравнение результатов

Диаграммы Венна:


<p float="left">
  <img src="/pictures/v1.png" width="400" />
  <img src="/pictures/v2.png" width="400" />
</p>

```
Q: Как можно объяснить различия в количестве пересечений?
A: Различия появляются, потому что сначала мы накладываем одни участки на другие, 
а потом вторые на первые... 
```
