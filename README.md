# コンテナをpodで実行
```
# コマンドでイメージ指定して起動(runは動くが非推奨)
kubectl create deployment webserver --image=nginx --replicas=5
kubectl run hello-world --image=hello-world -it --restart=Never

# 設定ファイル適用
kubectl apply -f sample_nginx.yml
# 自作dockerイメージを使う場合はDockerfileを使ってdocker buildして付けたtagをマニフェストで指定
```

# コンテナでpodやworkloadを削除
```
kubectl delete deployment webserver

kubectl delete -f sample_nginx.yml
```

# ステータス確認
```
# pod状況確認
kubectl get pod

# ipなどを含めた状況確認
kubectl get pod -o wide

# ログ確認
kubectl logs hello-world

# podの立ち上げ状況を見る
kubectl describe hello-world

# 全情報見る
kubectl get all

# pod内コンテナにアクセス
kubectl exec -it (pod名) -c (コンテナ名) -- (コマンド)
kubectl exec -it init-sample -c main -- sh
```

# 各機能の関係性
マシンからインターネットに向かって説明
（正しさよりも、忘れやすい概念について簡易説明する）

- pod
  - コンテナをくくる単位
- controller
  - podに独自の役割を与える（deployment, jobなど）
  - deployment
    - マニフェストspec内のtemplate欄でpodの仕様を記載する
- workload
  - podをくくる単位
- node
  - マシン
- service
  - pod群への受付窓口
  - privateネットワークをpublicネットワークと接続する
- ingress
  - URL解決とかwebのアプリケーションの最前面でリッチなことをする
