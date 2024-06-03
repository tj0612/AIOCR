# なにこれ
AIOCRの技術について、まぁなんかbounding box決めてCNNとかtransformerでなんかやるんだろうなぁ、くらいの理解しかなかったので勉強スタート

# OCRの後処理について
OCR単体での精度はあまり良くないので後処理としてOCRの結果をNNで直すタスクがあるらしい。

読んだ論文：http://arxiv.org/abs/2108.02899v1 (Document Intelligence Workshop at KDD, 2021)

![後処理モデルのアーキテクチャ](image.png)

文字のembeddingを作ってそれを1d convに入れて、その出力を2種類の全結合層にぶち込む。片方はInsert, Replace, Insert_Space, Deleteの多クラス分類を解いて、もう片方は何の文字をInsert（Replace）するかを予測するモデル。lossはハイパーパラメータ$\alpha,\beta$を用いて$L = \alpha * L_{action} + \beta * L_{character}$とする。