# webdb110-cookpad-sre-example
このレポジトリは、2019年4月25日発売の[WEB+DB PRESS Vol.110](http://gihyo.jp/magazine/wdpress/archive/2019/vol110)に掲載されている 「大規模インフラ解体新書」連載のサンプル設定です。

設定は [envoy/example/front-proxy](https://github.com/envoyproxy/envoy/tree/adda57914297f4179ae29e4bb34685124f3e516b/examples/front-proxy) および WEB+DB PRESS Vol.107 のサンプルである [rrreeeyyy/service-mesh-example](https://github.com/rrreeeyyy/service-mesh-example) をベースとしています。

# サンプルの利用方法
本サンプルの利用には Docker 環境が必要です。

本誌で紹介した設定のうち、 fault injection に関する設定を除いた設定が `./front-envoy.yaml` に、
fault injection を利用している設定が `./front-envoy-with-fault-injection.yaml` に記載してあります。

```
$ docker-compose up --build
```

で起動し、

```
$ curl localhost:8000/service/1
```

でアクセス可能です。

## 設定切り替え
fault injection に関する機能を試したい場合、docker-compose.yaml において、

```yaml
    volumes:
      - ./front-envoy.yaml:/etc/front-envoy.yaml
    # With fault injection configuration
    #  - ./front-envoy-with-fault-injection.yaml:/etc/front-envoy.yaml
```

この設定を以下のように書き換えてください。

```yaml
    volumes:
    #  - ./front-envoy.yaml:/etc/front-envoy.yaml
    # With fault injection configuration
      - ./front-envoy-with-fault-injection.yaml:/etc/front-envoy.yaml
```
