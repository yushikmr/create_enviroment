FROM python:3.9.5


ARG USERNAME=user
ARG GROUPNAME=user
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID $GROUPNAME && \
    useradd -m -s /bin/bash -u $UID -g $GID $USERNAME

COPY . /home/$USERNAME
WORKDIR /home/$USERNAME
ENV PYTHONPATH="/home$USERNAME:$PYTHONPATH"

RUN chown -R $USERNAME /home

USER $USERNAME

SHELL ["/bin/bash", "--login", "-c"]

RUN ["/bin/bash", "-c", "python -m venv venv"]

RUN ["/bin/bash", "-c", "/home/$USERNAME/venv/bin/python -m pip install --upgrade pip"]
RUN ["/bin/bash", "-c", "/home/$USERNAME/venv/bin/pip install -r requirements.txt"]

CMD ["/bin/bash", "-c", "/home/user/venv/bin/jupyter lab  --ip=0.0.0.0  --NotebookApp.token='' "]
