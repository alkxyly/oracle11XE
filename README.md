🧩 1. Contexto importante

Oracle 11g XE é gratuito, mas não é redistribuível — você não pode baixar uma imagem pronta de terceiros e usá-la legalmente.

A Oracle fornece scripts oficiais no GitHub para construir sua própria imagem Docker localmente.

O repositório oficial é:
🔗 https://github.com/oracle/docker-images

⚙️ 2. Passos oficiais (forma segura e legal)
🧱 Passo 1 — Clonar o repositório oficial da Oracle
git clone https://github.com/oracle/docker-images.git
cd docker-images/OracleDatabase/SingleInstance

🗂️ Passo 2 — Baixar o instalador do Oracle XE 11g

Você precisa baixar manualmente o .rpm do Oracle XE 11g, pois o script não faz o download automaticamente (licença Oracle).

Vá para o site oficial da Oracle:
🔗 https://www.oracle.com/database/technologies/xe-prior-release-downloads.html

Baixe o arquivo RPM correspondente a sua arquitetura (exemplo: oracle-xe-11.2.0-1.0.x86_64.rpm.zip).

Coloque esse arquivo dentro da pasta:

docker-images/OracleDatabase/SingleInstance/dockerfiles/11.2.0.2/

⚒️ Passo 3 — Construir a imagem Docker

Depois de copiar o instalador, execute:

cd dockerfiles
./buildContainerImage.sh -v 11.2.0.2 -x


O parâmetro -v define a versão.

O -x indica que é a edição XE (Express Edition).

🧠 Dica: O script vai criar automaticamente a imagem, por exemplo:

oracle/database:11.2.0.2-xe

🚀 3. Executar o container

Depois da build:

docker run -d \
  --name oracle-xe \
  -p 1521:1521 -p 8080:8080 \
  -e ORACLE_PWD=YourPassword123 \
  --shm-size=1g \
  oracle/database:11.2.0.2-xe
