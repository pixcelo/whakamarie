---
tags:
  - Python
---

# Python joblibを用いた高速化(処理の並列化・キャッシュ)

`joblib`は、大規模なデータを効率的に扱うためのPythonライブラリ

タスクを順次実行するのではなく、パイプラインを使用して並列実行することで高速化を実現する

## joblibの特徴

- メモリ内で処理できない大規模なデータをファイルに保存して読み込む
- 複数のコアを使用して並列処理を行う
- 処理済みの結果をキャッシュすることで、再利用する

機械学習のモデルをトレーニングする際のデータが大規模である場合、`joblib`を使用することで、データを分割して並列処理を行うことができる

処理済みの結果をキャッシュすることで、同じデータで再度トレーニングを行う場合には、処理をスキップできる

## Install

```
pip install joblib
```

## Usage

### Parallelクラス

`Parallel`クラスで処理を並列化する

```py
import math
import time
from joblib import Parallel, delayed

t2 = time.time()
# n_jobsはCPUのコア数を指定 (-1を引数に渡すと最大限のコア数を使用する)
result = Parallel(n_jobs=2)(delayed(math.factorial)(x) for x in range(8000))
t1 = time.time()

print(t2-t1) # 5.432750225067139
```

### Memoryクラス

`Memory`クラスでキャッシュする

```py
from joblib import Memory

# ディレクトリを指定
cachedir = './cache'
memory = Memory(cachedir, verbose=0)

# デコレータを定義
@memory.cache
def f(x):
    print('Running f(%s)' % x)
    return x

print(f(1)) # 関数に同じ引数を渡した場合、2回目以降は出力の結果のみが返る
```

## Reference
- [jonlib](https://joblib.readthedocs.io/en/latest/)
- [Parallel](https://joblib.readthedocs.io/en/latest/parallel.html)
- [Memory](https://joblib.readthedocs.io/en/latest/memory.html#module-joblib.memory)