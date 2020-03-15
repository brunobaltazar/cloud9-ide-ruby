# IDE Ruby on Rails Cloud9

Trata-se de uma imagem do Ubuntu 18.04 64 bits em Docker contendo um ambiente de desenvolvimento em Ruby on Rails pronto para utilizar.

Não é necessário a instalação de dependências pois já vem todo configurado no padrão Rails AppRef.
A imagem possui uma IDE open-source da Amazon chamada Cloud9 e deve ser iniciada utilizando docker-compose padrão.

----


# Dependências da imagem

  - Ruby 2.4
  - Rails 5.1
  - Yarn 1.12.3
  - Bundler 2.1
  - instantclient-basic-linux.x64-12.2.0.1.0
  - instantclient-sdk-linux.x64-12.2.0.1.0
  - instantclient-sqlplus-linux.x64-12.2.0.1.0
  - psql (PostgreSQL) 11.7
  - rvm 1.29


### Instalação

- Executar o comando de instalação do Docker Engine  - Community: 
 
 
     **sudo apt-get install docker-ce docker-ce-cli containerd.io**


- Verificar se o *Docker Engine - Community* está instalado corretamente executando a *imagem hello-world*: 

  
      **sudo docker run hello-world**
   

- Criar o grupo docker para realizar comandos sem sudo


    **sudo groupadd docker**
 

- Para adicionar o usuário ao grupo do docker:


    **sudo usermod -aG docker $USER**


- Fazer o *logout* e  *login* novamente para que o grupo seja atualizado caso .


- Verifique se você pode executar comandos sem **sudo** caso não funcione reniciar a maquina e testa novamente:

    **docker run hello-world**
    

- Clonar o projeto do git:
  
    


    **git clone https://github.com/brunobaltazar/cloud9-ide-ruby.git**




- Instalar o docker-compose:

    
       
       <https://docs.docker.com/compose/install/>
    
    

# Como utilizar


- Baixar a imagem do docker do repositório local utilizando o comando abaixo:
  
     **docker pull ide-c9:ruby_on_rails_5.1**

- Entrar na pasta do projeto
    
    exemplo:

    **/home/$USER/ide_ruby_on_rails_c9/cloud9-ide-ruby**     


- Realizar o seguinte comando:

     
     **docker-compose up build**

 

## Orientação iniciais
        

- Após iniciar o container, digitar http://localhost:8000/;

- Seu usário irar logar com o abc no console do cloud9;

- No container foi criado um usuário local chamado **rails** e para logar com este usuário basta digitar **"su - rails"** no terminal;

- Caso necessite de executar algum comando sudo com o usuário rails, a senha é *"rails"*

- Lembre-se, por ser um container o mesmo será destruido após pará-lo, porém ele faz um compartilhamento de arquivos entre sua maquina local e container docker localizado em /home/tj.ce.gov.br/${USER}/docker/dev 


# Importante:

-**Para subir a aplicação basta realizar o comando de build e por fim rails s -b 0.0.0.0**
        
-**Para subir o container usar o comando docker-compose up --build**
        
-**Para remover o container usar o comando docker-compose down**
        
 -**Para subir o container usar o comando docker-compose up --build**

        
        
        

# cloud9-ide-ruby
https://docs.aws.amazon.com/cloud9/latest/user-guide/sample-docker.html
https://github.com/c9/templates/blob/master/ws-ruby/Dockerfile
https://github.com/pwnlabs/oracle-instantclient