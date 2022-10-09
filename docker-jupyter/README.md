# docker-composeによるjupyter環境構築

- Dockerfile
- docker-compose.yml
- requirements.txt


## jupyter起動方法

- Dockerfile
- docker-compose.yml
- requirements.txt
があるディレクトリに移動し、

```bash
sudo docker-compose up -d
```
で起動完了. 初回だけイメージの作成が必要で時間がかかるが、2回目以降はすぐできる.

起動したら`http://ホストマシンのip:8888`でjupyter serverに接続できる
passwordが要求される可能性もあるがもあるが何も入力しなくてもログインできる. 


## image

元イメージは[dockerhub python 3.9.5 ](https://hub.docker.com/layers/library/python/3.9.5/images/sha256-5397e0aa0677c214bdbd6efecc9c8ec407e6a0f60715a7db1326e6b8c2b3fd37?context=explore).

pythonを元に`python -m venv`で`requirements.txt`からパッケージをインストール.

コンテナ起動時に
```Dockerfile
CMD ["/bin/bash", "-c", "/home/user/venv/bin/jupyter lab  --ip=0.0.0.0  --NotebookApp.token='' "]
```

でjupyter serverを立てる

## コンテナの起動

portは`8888:8888`をつないでいるため、ホストマシンもそのまま8888の接続で良い


```docker-compose.yml
    volumes: 
        - .:/home/user/
```
でホストマシンのカレントディレクトリをコンテナの`/home/user/`にマウントしている.

