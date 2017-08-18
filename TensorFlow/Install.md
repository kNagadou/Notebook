# TensorFlow Server構築
以下手順で作成したDokcerイメージ→ https://hub.docker.com/r/knagadou/tensorflow-server/

## Docker環境準備
* TensorFlow ServingのDocker手順を参考に https://www.tensorflow.org/serving/docker

### Create Dockerfile
* [Dockerfile.devel](https://github.com/tensorflow/serving/blob/master/tensorflow_serving/tools/docker/Dockerfile.devel)を修正し、新規Dockerfileを作成

[Dockerfile](Dockerfile)

### Build Container
* 上記で作成した `Dockerfile` があるディレクトリで、下記コマンドを実行する。

```
docker build --pull -t $USER/tensorflow-server-devel -f Dockerfile .
```

### Run Container

```
docker run -it $USER/tensorflow-server-devel
```

## Config TensorFlow
* TensorFlowをソースからビルドする手順を参考に https://www.tensorflow.org/install/install_sources

```
git clone https://github.com/tensorflow/tensorflow
cd tensorflow
git checkout r1.3 # Stable
./configure
```

### Build TensorFlow
* `--jobs 2` オプションを指定しないと、メモリ不足でビルドが失敗することがある。
   * マシンパワーに余裕がある場合は、もう少し上の数値を指定しても良いかもしれない。

```
bazel build --jobs 2 --config=opt //tensorflow/tools/pip_package:build_pip_package
bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
```

### Build TensorFlow Server
* 上記と同じく、 `--jobs 2` オプションは指定した方が良い。

```
bazel build --jobs 2 -c opt //tensorflow/core/distributed_runtime/rpc:grpc_tensorflow_server
```

## Validate

### Server

* Single
```
cd tensorflow
bazel-bin/tensorflow/core/distributed_runtime/rpc/grpc_tensorflow_server --cluster_spec='local|localhost:2222' --job_name=local --task_id=0
```

* Cluster
```
bazel-bin/tensorflow/core/distributed_runtime/rpc/grpc_tensorflow_server --cluster_spec='master|localhost:2222,worker|localhost:2223' --job_name=master --task_id=0 > master.log &
bazel-bin/tensorflow/core/distributed_runtime/rpc/grpc_tensorflow_server --cluster_spec='master|localhost:2222,worker|localhost:2223' --job_name=worker --task_id=0 > worker.log &
```

### Client
```
python
>>> import tensorflow as tf
>>> c = tf.constant("Hello, distributed TensorFlow!")
>>> sess = tf.Session("grpc://<server ip>:2222")
>>> sess.run(c)
'Hello, distributed TensorFlow!'
```