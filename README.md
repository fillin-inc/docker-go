# docker-go

Go 言語の Docker ベースイメージ管理リポジトリです。

株式会社フィルインでは AWS Lambda を利用したサーバレスアプリケーションを Go 言語ベースで開発しています。
ベースイメージとして　[debian](https://hub.docker.com/_/debian) の `*-slim` イメージをベースとして Go のイメージを作成し利用しています。

## 使い方

### 単独

```sh
$ docker run --rm -it ghcr.io/fillin-inc/go:1.16.5-bullseye-slim bash
```

## Multi Stage Build

Go 言語の場合、単独のバイナリを生成可能なためリリース時に [Multi-Stage Build](https://docs.docker.com/develop/develop-images/multistage-build/) を利用して軽量な　Docker イメージを作成します。

```dockerfile
FROM ghcr.io/fillin-inc/go:1.16.5-bullseye-slim

RUN go env -w GOPROXY=direct
ADD go.mod go.sum /
RUN go mod download
ADD . /
RUN cd /; make build

FROM debian:bullseye-slim
COPY --from=build /path/to/app /bin/app
ENTRYPOINT [ "/bin/app" ]
```
