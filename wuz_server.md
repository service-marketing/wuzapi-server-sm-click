- Baixa o git e o golang
sudo apt update
sudo apt install git -y
sudo apt install golang-go

- Configure com suas credenciais
git config --global user.name ""
git config --global user.email ""

- Clone o repositório: https://github.com/guilhermejansen/wuzapi.git

- Instalar o postgresql
sudo apt install postgresql postgresql-contrib -y

- Entrar no postgres e criar um banco de dados
sudo -i -u postgres
psql

CREATE DATABASE wuzapi;

- Por fim, sair do postgres
\q
exit

- Caso tenha que redefinir a senha do usuário
sudo -i -u postgres 
psql
ALTER USER seu_usuario WITH PASSWORD 'nova_senha';
\q
exit


- Instalar uma versão especifica do whatsmeow
go get go.mau.fi/whatsmeow@v0.0.0-20250402091807-b0caa1b76088

- Por meio do comando ```nago go.mod```, modifique o arquivo inteiro para este:

module wuzapi

go 1.23.0

toolchain go1.23.1

require (
	github.com/go-resty/resty/v2 v2.11.0
	github.com/gorilla/mux v1.8.0
	github.com/justinas/alice v1.2.0
	github.com/mdp/qrterminal/v3 v3.0.0
	github.com/nfnt/resize v0.0.0-20180221191011-83c6a9932646
	github.com/patrickmn/go-cache v2.1.0+incompatible
	github.com/rs/zerolog v1.33.0
	github.com/skip2/go-qrcode v0.0.0-20200617195104-da1b6568686e
	github.com/vincent-petithory/dataurl v1.0.0
	go.mau.fi/whatsmeow v0.0.0-20250318233852-06705625cf82
	google.golang.org/protobuf v1.36.5
)

require github.com/lib/pq v1.10.9

require (
	github.com/google/go-cmp v0.6.0 // indirect
	golang.org/x/time v0.5.0 // indirect
)

require (
	filippo.io/edwards25519 v1.1.0 // indirect
	github.com/google/uuid v1.6.0 // indirect
	github.com/gorilla/websocket v1.5.0 // indirect
	github.com/jmoiron/sqlx v1.4.0
	github.com/joho/godotenv v1.5.1
	github.com/mattn/go-colorable v0.1.13 // indirect
	github.com/mattn/go-isatty v0.0.19 // indirect
	github.com/rs/xid v1.6.0 // indirect
	go.mau.fi/libsignal v0.1.2 // indirect
	go.mau.fi/util v0.8.6 // indirect
	golang.org/x/crypto v0.36.0 // indirect
	golang.org/x/net v0.37.0 // indirect
	golang.org/x/sys v0.31.0 // indirect
	rsc.io/qr v0.2.0 // indirect
)


- Crie um arquivo chamado de systemd
sudo nano systemd/system/wuzapi.service

- Adicione:
[Unit]
Description=Wuzapi Service
After=network.target

[Service]
Type=simple
User=seu_usuario
WorkingDirectory=/{{{caminho/completo/para/repositorio}}}
ExecStart=/{{{caminho/completo/para/repositorio/wuzapi}}}
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target


- Recarregue o systemd, habilite e inicie o serviço:

sudo systemctl daemon-reload
sudo systemctl enable wuzapi
sudo systemctl start wuzapi