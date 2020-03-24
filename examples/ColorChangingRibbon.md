<!-- NeosVR Techbook-->

# 色の変わるリボン

## 概要

リボンの色が時間とともに変わっています。これを行うLogiXを紹介します。

ORANGEさんの[動画](https://www.youtube.com/watch?v=Bhg2zbBQUoY&feature=youtu.be)があります。3分で、すべてがまとまっているので、是非ご覧ください。

<img src="https://pbs.twimg.com/media/ETjQmBDUcAAT3wH?format=jpg" width=100px>

<img src="https://pbs.twimg.com/media/ETjQmBYUYAIE0xt?format=jpg" width=100px>

## 解説
[T/10](https://neosvrjp.memo.wiki/d/T/10)を使って、これまでの経過時間の1/10の数字を秒で取り出します。これを正弦関数を通して-1から1までの数値に変えます。HSVは色相(Hue)、彩度(Saturation・Chroma)、明度(Value・Brightness)となっています。LogiXでは0から1の数値を入れるようになっているようです。数値からHSVを作るのが[From HSV](https://neosvrjp.memo.wiki/d/FromHSV)です。これで黄色い帯のcolor型の情報をつくります。

これをリボンのインタフェースノードであるPBS_MetallicのEmissiveColorに入れています。AlbedoColorに入力するとドキドキした色では無くて落ち着いた色になります。

LogiXではノードにLogiXツールの先端を当てて帯を引き出し、さらにセカンダリーアクションを押すことで、値を観測するノードを作ることができます。ここではSinの出力値と、HSVがどのような色になるのかというのが表示されています。

![pic](https://pbs.twimg.com/media/ETjQmBpUUAABt0w?format=jpg&name=large "pic")

## おわりに
よく紹介されるデモです。周期的に色や大きさなどを変えるときに利用できそうですね。