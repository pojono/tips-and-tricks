# Tips-And-Tricks

## Запустить web-сервер на локальном компьютере

1. Open terminal or cmd and install the `http-server` module globally on your machine
  ```
  npm i -g http-server 
  ```
3. Run it using CLI (specifying the folder you'd like to serve files from)
  ```
  http-server ./[yourfolder] -p 1337
  ```
4. Now you should be able to access your files (via something like http://localhost:1337/myfile.html) in a web browser.

## Расшарить локальный порт
1. Download ngrok: https://dashboard.ngrok.com/get-started/setup
2. Unzip it:
  ```
  unzip /path/to/ngrok.zip
  ```
3. Running this command will add your authtoken to the default ngrok.yml configuration file. This will grant you access to more features and longer session times. Running tunnels will be listed on the status page of the dashboard.
  ```
  ./ngrok authtoken YOUR_TOKEN
  ```
4. To start a HTTP tunnel forwarding to your local port 80, run this next:
  ```
  ./ngrok http 80
  ```
  Or tcp forwarging:
  ```
  ./ngrok tcp 8080
  ```
## Сменить remote у git репозитория:
https://help.github.com/en/github/using-git/changing-a-remotes-url

## Узнать какая папка занимает место на жестком диске:
```
sudo du -sm * | sort -n
```

## Исправить ID в базе Postgres (например таблица quiz)

SELECT MAX(id) FROM quiz;

select (SELECT MAX(id) FROM quiz) + 1;

SELECT pg_catalog.setval(pg_get_serial_sequence('quiz', 'id'),(SELECT MAX(id) FROM quiz) + 1);

## Разрешить авторизацию паролем
https://serverpilot.io/docs/how-to-enable-ssh-password-authentication/

## Сделать zip архив из папки

zip -r data.zip ./data/

## Сделать zip архив из папки, исключая определенные папки

zip -r data.zip data -x "data/ignoreDir1/*" "data/ignoreDir2/*"

## Распаковать zip архив

unzip data.zip -d ./destination-folder

## Скачать файл с удаленного сервера

scp -i ~/key.pem USER@HOST:/remote-path/data.zip ~/local-path/

## Save docker logs to file

docker logs -f <yourContainer> &> your.log &

## Установка AWS CLI 2
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

sudo ./aws/install

## Настройка jenkins
docker exec -it jenkins bash;
adduser jenkins docker;
exit;
docker exec -u jenkins -it jenkins bash;
aws configure;
aws ecr get-login-password \
    --region eu-west-1 \
| docker login \
    --username AWS \
    --password-stdin ACCOUNT_ID.dkr.ecr.eu-west-1.amazonaws.com

## Распознавание добавленного объема жесткого диска
https://linuxhint.com/increase-disk-space-ec2/
  
growpart /dev/vda 2

resize2fs /dev/vda2

## Установка ansible-playbook

$ sudo apt update
$ sudo apt install software-properties-common
$ sudo apt-add-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible

## Установка sshpass

$ apt-get install sshpass

## Настройка python для ansible
sudo ln -s /usr/bin/python3 /usr/bin/python

## Подключение по SSH без ввода пароля:
  1. Один раз сгенерировать ключ: https://git-scm.com/book/ru/v2/Git-на-сервере-Генерация-открытого-SSH-ключа
  2. Выполнить команду: 
ssh-copy-id -i ~/.ssh/id_rsa.pub user@host
  
## Диагностика подключения к БД

  docker run --name mypg -p 5432:5432 -e POSTGRES_PASSWORD=postgres -d postgres:11

  docker exec -it mypg bash

  while true; do pg_isready -d <DATABASE_NAME> -h <HOST> -p <PORT> -U <USERNAME>;date ; sleep 5; done

 ## Install Docker
  
curl -fsSL https://get.docker.com -o get-docker.sh
  
sudo sh get-docker.sh
  
sudo groupadd docker
  
sudo usermod -aG docker $USER

sudo curl -L "https://github.com/docker/compose/releases/download/2.1.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  
sudo chmod +x /usr/local/bin/docker-compose
  
## Install Brew for Mac M1
  
arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

alias brew="arch -x86_64 brew"

## Check ports on MacOS
  
  sudo lsof -iTCP -sTCP:LISTEN -n -P
  
  ps -eaf | grep `lsof -t -i:7000`

## Stop and remove Docker containers
  
docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)
