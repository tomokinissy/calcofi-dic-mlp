# CalCOFI DIC prediction with an MLP

Kaggle「[EDS 232 Ocean chemistry prediction for CalCOFI](https://www.kaggle.com/competitions/eds-232-ocean-chemistry-prediction-for-calcofi)」で、海水の溶存無機炭素(DIC)を予測したノートブックです。授業の実装課題として、モデルは順伝播型ニューラルネット(MLP)だけを使っています。

- スコア(RMSE): Private 3.46799 / Public 3.79668
- 交差検証(4分割 × 2回・全行の RMSE): 4.720
- モデル: tanh の小さな MLP(24-12 / 12-6 / 48-24)を NumPy で実装し、L-BFGS で全データ一括学習
- 損失: 外れ値に強い pseudo-Huber 損失 + L2 正則化
- 入力: 元の列(深さ・栄養塩は対数)、一部のモデルは観測地点(緯度経度を丸めたもの)の one-hot
- 地点の one-hot は学習側に 2 回以上出る地点だけ作り、値は 0.2〜0.25 に抑える
- 設定と乱数の種を変えた 18 本の予測を平均

## 実行方法

Kaggle Notebook にコンペのデータを追加して、上から順に実行します(GPU 不要。CPU で交差検証込み約 20 分、`RUN_CV = False` なら約 3 分)。データはコンペのページから取得してください。このリポジトリには含めていません。
