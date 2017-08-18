# インターン事前準備
今回のインターン課題は、PCにDockerとTensorFlowがインストールされている前提で進めます。 **本資料内ではDockerとTensorFlowの説明は省略しますので、各自でググってください。**

## Dockerインストール
macOSとWindowsで若干手順が異なります。

### macOS
* インストール
   * 下記リンクから、Stable Channelのインストーラーをダウンロードして実行。
   * https://docs.docker.com/docker-for-mac/install/
* Docker動作確認
   * `Docker.app` を起動し、続けて `Terminal.app` を起動。
   * `Terminal.app` で `docker` コマンドを入力し、Dockerの使用法が表示されることを確認。

### Windows
* 下記リンクから、Docker Toolboxをダウンロードして実行。
   * https://www.docker.com/products/docker-toolbox
* `Docker Quicstart Terminal` が起動することを確認。

## Dockerイメージのダウンロードとコンテナ起動
* **macOS** の場合は `Terminal.app` 、 **Windows** の場合は `Docker Quicstart Terminal` をそれぞれ起動し、下記コマンドを実行。
* イメージサイズが **4GB** 近くありますので、ディスクの空き容量に注意してください。

```sh
# https://hub.docker.com/r/knagadou/tensorflow-server/ からイメージをPull
docker pull knagadou/tensorflow-server
# コンテナを起動
docker run -dit knagadou/tensorflow-server
# コンテナが起動されたかを確認
docker ps
# 次のステップで{CONTAINER ID}を使用するため、控えておく
```

## TensorFlow動作確認
下記サンプルコードを実行してみます。

* 起動中のコンテナに接続

```sh
docker attach {CONTAINER ID}
```

* コンテナに接続出来たら、コンテナ上でサンプルコードを実行

```python
python

>>import tensorflow as tf
>>c = tf.constant("Hello, TensorFlow!")
>>sess = tf.Session()
>>sess.run(c)

# Hello, TensorFlow! と表示されればOK
```

## **Challenge** : TensorFlow Tutorials
TensorFlowの[公式ページ](https://www.tensorflow.org/tutorials/)に各チュートリアルが用意されています。今回のインターンでは自然言語処理を扱う予定ですので、以下のチュートリアルをオススメします。

* Word2vec
   * https://www.tensorflow.org/tutorials/word2vec
* Recurrent Neural Networks
   * https://www.tensorflow.org/tutorials/recurrent
* Sequence to Sequence
   * https://www.tensorflow.org/tutorials/seq2seq