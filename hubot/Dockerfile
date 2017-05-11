FROM node:latest
MAINTAINER Jordan Jethwa

# Environment variables
ENV DEBIAN_FRONTEND noninteractive

RUN useradd hubot -m

RUN mkdir /root/.config/
RUN mkdir /root/.config/configstore/
RUN chmod -R g+rwx /root /root/.config /root/.config/configstore
RUN apt-get update && apt-get -y install libicu-dev
RUN npm install -g yo --allow-root generator-hubot coffee-script --save
USER hubot

WORKDIR /home/hubot

RUN yo hubot --owner="o" --name="n" --description="desc" --defaults && \
 sed -i /heroku/d ./external-scripts.json && \
 sed -i /redis-brain/d ./external-scripts.json && \
 npm install hubot-scripts &&  \
 npm install hubot-irc --save

CMD node -e "console.log(JSON.stringify('$EXTERNAL_SCRIPTS'.split(',')))" > external-scripts.json && \
	npm install $(node -e "console.log('$EXTERNAL_SCRIPTS'.split(',').join(' '))") && \
	bin/hubot -a irc
