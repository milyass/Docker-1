FROM ubuntu
RUN apt-get update && apt-get upgrade -y
RUN apt-get install ca-certificates openssh-server wget -y
RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh
RUN chmod 777 script.deb.sh
RUN ./script.deb.sh
RUN apt-get install gitlab-ce -y
RUN DEBIAN_FRONTEND=noninteractive apt install -y tzdata
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/ */tmp/* /var/tmp/*
WORKDIR /etc/gitlab
RUN echo "external_url 'https://10.11.4.15'" > gitlab.rb
RUN echo "nginx['enable'] = true" >> gitlab.rb
RUN echo "nginx['redirect_http_to_https'] = true" >> gitlab.rb
RUN echo "nginx['redirect_http_to_https_port'] = 80" >> gitlab.rb
RUN echo "service ssh start" > script.sh
RUN echo "(/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && tail -f /dev/null" >> script.sh
RUN chmod 700 script.sh
ENTRYPOINT ./script.sh
#docker run -it -p 10.11.4.15:443:443 -p 10.11.4.15:80:80 -p 10.11.4.15:22:22 gitlb
#git config --global http.sslVerify false
