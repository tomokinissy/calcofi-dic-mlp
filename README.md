# CalCOFI DIC prediction with an MLP

Kaggle「[EDS 232 Ocean chemistry prediction for CalCOFI](https://www.kaggle.com/competitions/eds-232-ocean-chemistry-prediction-for-calcofi)」で、海水の溶存無機炭素(DIC)を予測したノートブックです。授業の実装課題として、モデルは順伝播型ニューラルネット(MLP)だけを使っています。

- スコア(RMSE): Private 4.10743 / Public 3.74564
- モデル: MLP 128-64(ReLU)、MSE、Adam(lr 3e-4, weight decay 3e-4)、コサイン減衰、3000 エポック
- 入力: 元の列、化学的な派生特徴(log 深さ・飽和酸素量・AOU・PO・NO・N*・PO4pre)、観測地点の one-hot
- 地点の one-hot は学習中 50% の確率でまとめて 0 にする(test にしかない地点に備える)
- 交差検証で残差が 4σ を超えた 17 行は学習から除外
- 乱数の種を変えた 20 本の予測を平均

## 実行方法

Kaggle Notebook にコンペのデータを追加して、上から順に実行します(GPU 推奨・T4 で約 45 分)。データはコンペのページから取得してください。このリポジトリには含めていません。
