# 機械学習 環境構築

## Python
* AnacondaでPython実行環境を用意する。
* Pythonのバージョン管理ができ、パッケージ管理システムが使え、仮想環境も作れるので凄く便利。
* Windows版も検証してみたい。

### [Anaconda](https://www.continuum.io/DOWNLOADS)
* インストーラーをDLして、インストールするだけで利用可能

## TensorFlow
* 環境構築の参考にした記事
  - http://qiita.com/isboj/items/3d62d7dc3f7a616de24e#13-%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%82%92%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B
  - 公式のMacインストール手順
    - https://www.tensorflow.org/install/install_mac
    - https://www.tensorflow.org/install/install_mac#the_url_of_the_tensorflow_python_package
* condaでpython3.5環境構築後、CPUサポート版TensorFlowをインストール
  - `pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.2.1-py3-none-any.whl`

## Chainer環境構築
* TensorFlowと同じく、condaでpython3.5環境構築してChainerをインストール
```sh
# Install
$ pip install chainer
# Sample MNIST
$ git clone https://github.com/pfnet/chainer.git
$ python chainer/examples/mnist/train_mnist.py
```

* `train_mnist.py`を実行する際に、numpy.lib.mixinsが無いと怒られる
  - numpyをuninstallして、再度installする

## Scikit-learn
* SLで出来ること
  - http://qiita.com/ynakayama/items/9c5867b6947aa41e9229
* 文字列のクラスタリングは以下記事を参考
  - http://qiita.com/yuuki_1204_/items/3c0a298a521dc6e79615#_reference-f2d5727defbd48fe3385
  - http://qiita.com/yuuki_1204_/items/c26cb09fba8aad35dc0a

## おまけ
* Mecab用の辞書。頻繁に更新されており便利
  - https://github.com/neologd/mecab-ipadic-neologd/blob/master/README.ja.md

## その他メモ
* TensorFlow、Chainer、Caffeはディープラーニングに特化したライブラリ。機械学習を幅広くやるなら、Scikit-learnか。
* macOSなら環境構築に手間取ることはないが、Windowsだとどうだろう。
* 上記の環境構築だけなら、TensorFlowとかChainerとか1つずつ環境作っても10分〜30分程度。サンプル（MNIST)の実行は30分〜1時間くらいかかる。
