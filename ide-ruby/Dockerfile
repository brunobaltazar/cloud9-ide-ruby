FROM linuxserver/cloud9:latest

#container build
#docker build --tag ide:1.0 .

############# certificates install #######################################################
RUN mkdir /usr/share/ca-certificates/TJCE
ADD ./TJCE_Internet.crt  ./TJCE_CA_Infraestrutura.crt  ./TJCE_CE_Intermediaria_Infra.crt  /usr/share/ca-certificates/TJCE/
RUN cp -R /usr/share/ca-certificates/TJCE  /usr/local/share/ca-certificates && update-ca-certificates

############# cliente oracle #######################################################
ENV LD_LIBRARY_PATH=/opt/oracle/instantclient_12_2/
RUN export LD_LIBRARY_PATH=/opt/oracle/instantclient_12_2/
RUN echo 'source /opt/oracle/instantclient_12_2/network/admin/.oracle' >> /etc/bash.bashrc

RUN mkdir -p /opt/oracle/instantclient_12_2/network/admin \
    && apt-get update \
    && apt-get -y  install unzip \
    && apt-get -y  install sudo

ADD ./instantclient-basic-linux.x64-12.2.0.1.0.zip ./instantclient-sdk-linux.x64-12.2.0.1.0.zip ./instantclient-sqlplus-linux.x64-12.2.0.1.0.zip     /opt/oracle/
ADD ./tnsnames.ora   ./.oracle       /opt/oracle/instantclient_12_2/network/admin/


RUN cd /opt/oracle \
 && unzip instantclient-basic-linux.x64-12.2.0.1.0.zip \
 && unzip instantclient-sdk-linux.x64-12.2.0.1.0.zip \
 && unzip instantclient-sqlplus-linux.x64-12.2.0.1.0.zip \
 && cd /opt/oracle/instantclient_12_2 && ln -s libclntsh.so.12.1 libclntsh.so

# ############# dependencias e softwares ########################################

RUN apt-get -y  install wget \
     && apt-get -y  install curl \
     && apt-get -y  install libcurl4-openssl-dev \
     && apt-get -y  install libpq-dev \
     && apt-get -y  install nano \
     && apt-get -y  install libaio1 \
     && apt-get -y install git

############### nodejs e yarn #########################################################

RUN apt-get -y install curl
RUN curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update

RUN apt-get -y install git-core \
zlib1g-dev \
build-essential \
libssl-dev \
libreadline-dev \
libyaml-dev \
libsqlite3-dev \
sqlite3 \
libxml2-dev \
libxslt1-dev \
libcurl4-openssl-dev \
software-properties-common \
libffi-dev \
nodejs \
yarn 


############### PostgreSQL ####################################################### 

RUN apt-get install curl ca-certificates gnupg
RUN wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add - 
RUN touch /etc/apt/sources.list.d/pgdg.list
RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN apt-get update
RUN apt-get -y install postgresql-11 pgadmin4

# ############### USER  ############################################################


#RUN useradd -m -u $UID -g $GID -o -s /bin/bash $UNAME
#RUN useradd -m -u $UID -g $GID -o -s /bin/bash $UNAME
#RUN useradd -m -u $UID -g $GID -o -s /bin/bash $UNAME

RUN useradd -m -u 1500 -g 27 -o -s /bin/bash rails
RUN echo 'rails ALL=NOPASSWD:ALL'>> /etc/sudoers
RUN mkdir -p /var/run/s6/services/s6-fdholderd/supervise/control
RUN chown rails -R /var/run/s6
RUN chmod 777 -R /var/run/s6
#  RUN useradd -ms /bin/bash rails \
#       #&& echo 'rails ALL=NOPASSWD:ALL'>> /etc/sudoers \
#       && echo 'rails:rails' | chpasswd \
#       && usermod -a -G rails rails \
#       && usermod -a -G sudo rails \
#       && usermod -a -G root rails \
#       && usermod -a -G users rails 



#RUN /bin/bash -l -c   'chown rails:rails -R /var/run/'


USER rails


# # install rails

# RUN  sudo apt install curl \
#  && curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash - \
#  && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - \
#  && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list \
#  && sudo apt-get update \
#  && sudo apt-get install git-core zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs yarn 

#  RUN sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev -y
# RUN sudo gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB 
#  && curl -sSL https://get.rvm.io | bash -s stable \
#  && source ~/.rvm/scripts/rvm \
#  && rvm install 2.7.0 \
#  && rvm use 2.7.0 --default \
#  && ruby -v


#RUN \curl -sSL https://rvm.io/mpapis.asc | gpg --import -
#RUN \curl -sSL https://get.rvm.io | bash -s stable --ruby
#ENV RUBY_VERSION 2.4.2
#ENV RAILS_VERSION 5.1.3
#RUN /bin/bash -l -c 'source /home/rails/.rvm/scripts/rvm'\
#  && /bin/bash -l -c "rvm install $RUBY_VERSION" \
#  && /bin/bash -l -c "rvm use $RUBY_VERSION --default" \
#  && /bin/bash -l -c 'rvm requirements' \
#  && /bin/bash -l -c 'rvm rubygems current' \
#  && /bin/bash -l -c "gem install rails --version=$RAILS_VERSION --no-ri --no-rdoc" \
#  && /bin/bash -l -c 'gem install bundler --no-ri --no-rdoc'

#RUN echo 'source /home/rails/.rvm/scripts/rvm' >> $HOME/.bashrc
#USER root