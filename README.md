# gco_smile

Para rodar a aplicação, se faz necessário versões antigas de apache2, php e mysql, 
como reescrever este código é um processo um pouco demorado,
nós podemos rodar ele nessa versão com um container Docker lamp 
com versões antigas das aplicações citadas acima, mas AVISO:
Não rode isso em produção de forma aberta pois existem diversas brechas 
de segurança nessas aplicações antigas que foram mitigadas em suas respectivas 
atualizações posteriores.
Portanto AVISO: rode isso apenas como teste ou em um ambiente com a rede estritamente 
controlada para o acesso a esta aplicação...

Devidos avisos feitos, vamos executar o Container:

###########Passo 1: Usando SO Linux #############

Crie uma pasta em seu pc com o comando mkdir qualquer_nome
Crie um arquivo com nome Dockerfile na pasta e cole o código abaixo dentro dele:

FROM tutum/lamp:latest
USER root
RUN rm -fr /app && git clone https://github.com/hck5/gco_smile.git /app
RUN chown -R root:root /app
RUN chmod -R 777 /app
EXPOSE 80 3306
CMD ["/run.sh"]


###########Passo 2 #################
rode os comandos abaixo estando dentro da pasta criada e com o Dockerfile criad

docker build -t username/my-lamp-app .             
ps: substitua o username pelo nome de seu usuário, ou por $USER
este comando irá construir o container com as instruções e comandos do arquivo Dockerfile

após, rode o container com o comando:
docker run -d -p 80:80 -p 3306:3306 username/my-lamp-app     
ps: troque o nome username pelo inserido no comando anterior                 

após isso, só acessar pelo navegador com a url:   http://127.0.0.1/index.php
instalar a aplicação, e tudo pronto...



dúvidas: https://hub.docker.com/r/tutum/lamp
