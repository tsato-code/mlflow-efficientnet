# KerasでEfficientNetの転移学習するプログラムをMLflowのパッケージにする

MLflow は機械学習モデルのライフサイクルを管理するツール。
以下のようなことができる。
- 実験周りのコードや設定・結果の記録
- どこでも再現できるようにするためのパッケージング
- モデルを各環境にデプロイするための方法やフォーマット
もちろんOSSで無料、Apache 2.0ライセンス。

今回、試しにKerasでEfficientNetを動かしてみたので、それをMLflowでパッケージ化して、実験管理をする。


## EfficientNet
参考にするのは次の記事。
- [【Keras】EfficientNetのファインチューニング例 | 旅行好きなソフトエンジニアの備忘録 プログラミングや技術関連のメモを始めました](http://ni4muraano.hatenablog.com/entry/2019/06/16/084011)

扱うデータセットはKaggleからダウンロード。
- [10 Monkey Species
Image dataset for fine-grain classification | Kaggle](https://www.kaggle.com/slothkong/10-monkey-species)


## NOTE
- 挙動を見ていると、conda.ymlのdependenciesでpip:ライブラリと書くと、conda仮想環境作成時にpipインストールされるらしい。
- `mlflow models serve -m runs:/<id>/model` でconda仮想環境を作るが、これは不要？
- tensorflow==1.15.2から1.14に変えたら、挙動が変わった。エラーが出ることに変わりはない。
- Keras==2.2.4から
- swishというdropout関連のエラーのように見える。
    - `ValueError: Unknown activation function:swish`
    - https://www.kaggle.com/c/bengaliai-cv19/discussion/134952

### 参考資料
- [MLflowでkerasモデルなどを管理してみた | Qiita](https://qiita.com/sumita_v09/items/174977f48c44244f9719)