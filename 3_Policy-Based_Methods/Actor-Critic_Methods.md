
https://sykwer.hatenablog.jp/entry/2018/03/10/Understand_DDPG_step_by_step_%282%29

- SPG(stcastic policy gradient)は、状態空間と行動空間の2つに対して期待値をとっているのに対して、
- DPG(deterministic policy gradient)は、状態空間のみに対して期待値をとっています.

# DPG
方策勾配は、行動価値関数の勾配の期待値

多くのmodel-freeを想定した強化学習アルゴリズムをざっくりまとめると、policy-evaluation -> policy-improvement -> policy-evaluation -> ... というようなpolicy-iterationのサイクルにしたがってアルゴリズムが進行していくと捉えることができます.
 
policy-evaluationのフェーズでは、行動価値関数Qμ(s,a)の評価を行います. 具体的には、モンテカルロ近似やTD学習によって評価されます.
 
policy-improvementのフェーズでは、policy-evaluationのフェーズで更新された行動価値関数にしたがって、方策を更新します. もっとも単純な具体例は、greedyアルゴリズムにしたがって方策を決定していくアプローチでしょう.

(k+1ステップにおける方策は、前のステップでevaluateされた行動価値関数に対するgreedyな選択によって決定する、という意味)
 
このgreedyな選択は、行動空間が離散でかつ次元数が小さいときは、大きすぎないルックアップテーブルから最大値を探す作業となり、コンピュータ上で計算可能です.
 
しかし、行動空間が連続である場合は argmaxaQμk(s,a)を毎ステップ、解析的に求めなくてはなりません. これは不可能です.
 
そこで思いつく有効な代替案は、方策のパラメータを行動価値関数Qの勾配の方向に更新するというものです.
 
つまり、方策のパラメータθk+1は∇θQμk(s,μθ(s))の方向に更新する、というアルゴリズムが導かれます.
 
