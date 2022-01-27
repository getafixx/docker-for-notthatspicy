FROM getafixx/php8-fpm

RUN groupadd --gid 1000 vscode \
	&& useradd --uid 1000 --gid vscode --shell /bin/bash --create-home -g root -G sudo  -G www-data vscode
# handy for Justin
COPY ./.bashrc /root/.bashrc
COPY ./.gitconfig /root/.gitconfig

RUN touch /root/.bash_history

#git ssh set up for pulling and pushing
RUN mkdir /root/.ssh
COPY ./.ssh/id* /root/.ssh/
RUN chmod -R 600  /root/.ssh

# handy for Justin
COPY ./.bashrc /home/vscode/.bashrc
COPY ./.gitconfig /home/vscode/.gitconfig

RUN touch /home/vscode/.bash_history

#git ssh set up for pulling and pushing
RUN mkdir /home/vscode/.ssh
COPY ./.ssh/id* /home/vscode/.ssh/
RUN chmod -R 600  /home/vscode/.ssh
RUN chown -R vscode:vscode  /home/vscode/


WORKDIR /workspaces/code/
