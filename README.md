# helm-repo


## Create you own helm chart
```
$ helm create mychart
```


編輯 ./mychart/values.yaml 更改 image path


* 產生 index.yaml
```
$ helm repo index .
``` 


* 製作 chart
```
$ helm package ./mychart
``` 
會打包成 chart 並且預設會放置在你的 ~/.helm/repository/local/ 下面


---
## Setup helm repository using GitHub Pages
* 先在 github 上面開好 repo (https://github.com/lmchih/helm-repo)
```
$ mkdir gitcharts 
$ cp ./mychart ./gitcharts
$ cp index.yaml ./gitcharts
```

此時你的 gitcharts 會有下列結構
```
gitcharts
|—— charts
|       |—— mychart-0.1.0.tgz
|___ index.yaml
```
(最後會將這包上傳 GitHub)

* 製作 gh-pages 分支
```
$ git init
$ git checkout -b gh-pages
$ git add -A
$ git commit
$ git push origin gh-pages
```

---
## Install your charts on any k8s cluster
去你的 repo settings 找到 GitHub Pages 那邊會有一個 url: https://lmchih.github.io/helm-repo
複製這個 url

```
$ helm repo add lmchih https://lmchih.github.io/helm-repo
```

```
$ helm search lmchih
NAME          	CHART VERSION	APP VERSION	DESCRIPTION                
lmchih/mychart	0.1.0        	1.0        	A Helm chart for Kubernetes
```

```
$ helm install lmchih/mychart
``` 
恭喜你成功用 helm 完成 mychart 的部署!
 
