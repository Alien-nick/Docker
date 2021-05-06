FROM debian

RUN apt-get update && apt-get -y install locales

RUN apt-get update \
    && apt-get -y install man sudo locate build-essential wget zsh

RUN apt-get -y install openjdk-8-jdk

RUN useradd -m burp

RUN echo "burp ALL=NOPASSWD: ALL" > /etc/sudoers.d/burp
RUN chsh -s /usr/bin/zsh burp

USER burp
RUN mkdir -p /home/burp/bin

RUN wget -O /home/burp/.zshrc https://git.grml.org/f/grml-etc-core/etc/zsh/zshrc
RUN echo "export PATH=/home/burp/bin:$PATH" >> /home/burp/.zshrc

WORKDIR /home/burp/bin

### Install Burpsuite ###
RUN wget -O ./burp.jar 'https://portswigger.net/DownloadUpdate.ashx?Product=Free' \
    && chmod +x ./burp.jar
RUN echo "#! /bin/bash \n\
java -jar /home/burp/bin/burp.jar > /dev/null 2>&1 & \n" > burpsuite \
    && chmod +x burpsuite

RUN sudo apt-get clean
WORKDIR /home/burp
CMD ["zsh", "-i"]
