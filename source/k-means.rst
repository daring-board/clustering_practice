.. _k-means:

.. toctree::
  :maxdepth: 4

KMeans
========================

KMeansとは
-------------------

  | KMeansはクラスタリングアルゴリズムであり、教師なし学習に分類される。
  | クラスタリングアルゴリズムは、階層型クラスタリングと非階層型クラスタリングの
  | ２種類があり、KMeansは非階層型クラスタリングである。

  | 階層型クラスタリング

  .. image:: ./img/layered_clustering.jpg
      :scale: 100%

  | https://www.albert2005.co.jp/knowledge/data_mining/cluster/hierarchical_clustering

  | 非階層型クラスタリング

  .. image:: ./img/kmeans.png
      :scale: 100%

  | https://pythondatascience.plavox.info/scikit-learn/%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%BF%E5%88%86%E6%9E%90-k-means

アルゴリズム
-------------------
  | KMeansは、すべての入力データ点とクラスタの重心との距離を最小化することで
  | 凝集したデータ点の集まりを一つのクラスタとして、分割するアルゴリズムである。
  | KMeansでは、クラスタに分割する個数を予め決めておく必要がある。
  | アルゴリズムの動作は以下である。

  1. データが含まれる空間にランダムにk個の点(セントロイド)を置き、それぞれのクラスタの中心とする
  2. 各データがセントロイドのうちどれに最も近いかを計算して、そのデータが所属するクラスタとする
  3. セントロイドの位置をそのクラスタに含まれるデータの重心になるように移動する
  4. 各セントロイドの位置が変わらなくなるまで2, 3を繰り返す

例
-----
  | PythonによるKMeansの実行例。
  | https://github.com/daring-board/clustering_practice/blob/master/KMeans.ipynb

実データへの適用
--------------------------
  | カメラのデータをKMeansにより分類する。
  | https://github.com/daring-board/clustering_practice/blob/master/CameraDataClustering.ipynb


数式表現
--------------------
  | 以下に、KMmeansアルゴリズムの数式表現を示す。

モデル式
^^^^^^^^^^^^^^^^^^
  | KMeansモデルによって出力データを予測する式。

  .. math::

    y = arg min_{j \in [K]} \{ (x - \mu_j)^2 | \mu_j \in \theta \}

  | 読み方：
  | 　パラメータ集合 :math:`\theta` に含まれるすべての重心点 :math:`\mu_j` に対して、
  | 　入力データ :math:`x` との距離が最小の重心点 :math:`\mu_j` のインデックス :math:`j` を
  | 　出力データ :math:`y` として返却する。


学習パラメータ更新式
^^^^^^^^^^^^^^^^^^^^^^^^^
  | KMeansモデルがパラメータを学習するための更新式。

  .. math::

    \mu_k = \frac{\sum_{n=1}^{N}r_{nk}x_n}{\sum_{n=1}^{N}r_{nk}} = \frac{\sum_{x_n \in C_k} x_n}{N_k}

  | これは :math:`\mu_k` はクラスタ内に含まれる入力データの平均値として更新されることを表している。

  | :math:`N_k` はクラスタ :math:`C_k` に含まれる入力データの個数。
  | :math:`r_{nk}` はデータ :math:`x_n` がクラスタ :math:`k` に属するとき1で、それ以外の場合は0とする。

  .. math::

    r_{nk} = \begin{cases}
      1 & (k = arg min_{j \in [K]} \{ (x - \mu_j)^2 | \mu_j \in \theta \}) \\
      0 & (otherwise)
    \end{cases}

更新式の導出
^^^^^^^^^^^^^^^^^^^^^^^^^

  | KMeansは、すべての入力データ点とクラスタの重心との距離を最小化するので、
  | 以下の数式を微分したものが上の更新式となる。

  .. math::

    \sum_{n=1}^{N} \sum_{k=1}^{K}r_{nk}(x_n-\mu_k)^2
