---
layout: post
title:  "Как использовать Tensorboard для Tensorflow с самого начала"
date:   2017-04-07 10:05:26 +0530
categories: tensorboard tensorflow beginner
---
Если открыть простейший [туториал по Tensorflow (TF)](https://www.tensorflow.org/get_started/get_started), можно встретить несколько примеров того, как простейшие сущности TF будут выглядеть в тулзе под названием `Tensorboard` (TB). TB - это визуализатор графа программы на TF, плюс куча вспомогательных инструментов, о которых мы узнаем позже, когда они нам понадобятся в более сложных программах. Но к сожалению, если мы, будучи новичками в TF пойдем в туториал TB чтоб повторить визуализацию только что изученых сущностей, мы наткнемся на пример довольно высокого уровня, который не особо поможет нам в запуске нашей первой программы.

Поэтому в этом посте мы рассмотрим необходимые шаги для запуска `Tensorboard` прямо в первых экспериментах с `Tensorflow`.

Нам понадобится установленый `Tensorflow` и `Tensorboard`:

{% highlight bash %}
$ pip install tensorflow
$ pip install tensorboard
{% endhighlight %}

Теперь давайте рассмотрим простейший пример программы на `Tensorflow`, в котором будут необходимые вызовы для визуализации в `Tensorboard`:

{% highlight python %}
import tensorflow as tf

with tf.Session() as sess:
  const1 = tf.constant(3.0, tf.float32, name='constA')
  const2 = tf.constant(4.0, dtype=tf.float32, name='constB')
  adder = tf.add(const1, const2, name='AddAB')

  init = tf.global_variables_initializer()
  sess.run(init)

  result = sess.run(adder)
  tf.summary.FileWriter('./log', sess.graph)
  print(result)
{% endhighlight %}

Результат следующий:
![AddAB пример]({{ site.url }}/screenshots/AddAB_tensorboard.png)

Я объясню это все позже.
