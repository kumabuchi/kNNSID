kNNSID
====

k-NN based Selective sampling method for Imbalanced Data  

2クラスラベル付きのImbalanceなデータセットから、その分布を考慮して未ラベル事例をサンプリングするプログラム。  
k-NNにより密な分布を維持しつつ、サンプリングされた事例との距離を評価して全域のサンプルを抽出する。  
  
####使用方法  
コンパイル  
javac kNNSID.java  
実行  
java kNNSID \<unlabeled_data_file\> \<minority_class_data_file\>  
  
####ファイルフォーマット  
[フォーマット1] 1次元の数値データ(1行に1データ)  
[フォーマット2] データID,数値データ のcsv形式。  
詳しくはサンプルデータを参照。  
  
####アルゴリズム  
　kNNSIDは、各未ラベル事例について評価関数で得られる評価値に基づいて、最も評価値が高い事例から順にサンプリングしていきます。Imbalanced Problemを含むデータセットでは、多くの場合サンプリング結果のほとんどが多数派クラスの事例となってしまいますが、分布をできるだけそのままに、少数派クラスからも事例をサンプリングするアルゴリズムです。  
　kNNSIDは事例を1つサンプリングするごとに各事例の評価値を再計算します。サンプリング済み事例との距離を評価値に反映させることで、多数派クラスの特定の分布のみからサンプリングされ続けることを避けます。評価値(score)を決める評価関数は以下の式で定義されます。  
  
*score= - avgDistKnn + avg(or sum)Dist*

avgDistKnn : 未ラベル事例と、少数派クラスのk-NN事例との平均距離  
avg(or sum)Dist : 未ラベル事例とサンプリング済み事例との平均(累積)距離  
  
プログラムの実装はavgDistで行なっています。  
評価値計算に累積距離を使いたい場合は、reCalcScore関数内のコメントアウト部分を入れ替えてください。  

