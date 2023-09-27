# estudos-airflow

Passo 1: Instale o Docker
Se você ainda não tiver o Docker instalado no Linux, siga as instruções abaixo:

Ubuntu:
sudo apt-get update
sudo apt-get install docker.io

Certifique-se de que o serviço Docker esteja em execução:
sudo systemctl start docker
sudo systemctl enable docker

Passo 2: Instale o Docker Compose
Você pode instalar o Docker Compose no Linux com os seguintes comandos:

sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

Verifique se o Docker Compose foi instalado corretamente executando:
docker-compose --version

Passo 3: Prepare seu ambiente de trabalho
Crie um diretório onde você deseja configurar seu ambiente do Apache Airflow com Docker:
mkdir airflow-docker
cd airflow-docker

Passo 4: Crie um arquivo docker-compose.yaml
Crie um arquivo chamado docker-compose.yaml no diretório que você acabou de criar e adicione o seguinte conteúdo:

version: '3'
services:
  webserver:
    image: puckel/docker-airflow:1.10.12
    ports:
      - "8080:8080"
    volumes:
      - ./dags:/usr/local/airflow/dags
    environment:
      - AIRFLOW__CORE__FERNET_KEY=myfernetkey
      - AIRFLOW__CORE__EXECUTOR=LocalExecutor
      - AIRFLOW__CORE__SQL_ALCHEMY_CONN=sqlite:////usr/local/airflow/airflow.db
    command: webserver
Este arquivo docker-compose.yaml configurará um contêiner Docker do Apache Airflow com as configurações básicas.

Passo 5: Inicie o Apache Airflow
Agora, inicie o Apache Airflow executando o seguinte comando no diretório onde você criou o arquivo docker-compose.yaml:

docker-compose up -d

O Apache Airflow deve começar a ser executado como um contêiner Docker em segundo plano.

Passo 6: Acesse o Apache Airflow Web UI
Abra um navegador da web e acesse http://localhost:8080 para acessar a interface web do Apache Airflow. Você pode fazer login com as credenciais padrão (username: admin, password: admin).

A partir daqui, você pode criar e gerenciar seus DAGs e tarefas do Apache Airflow usando a interface web.

Lembre-se de que este é um ambiente de desenvolvimento básico. Para ambientes de produção, você deve configurar um banco de dados mais robusto e configurar outras opções de segurança. 
Consulte a documentação do Apache Airflow para obter mais informações sobre como configurar e usar o Apache Airflow em um ambiente de produção: https://airflow.apache.org/docs/






