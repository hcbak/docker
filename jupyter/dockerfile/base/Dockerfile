FROM ubuntu:latest

SHELL ["/bin/bash", "-c"]

# 변수 설정
ARG DEBIAN_FRONTEND=noninteractive
ARG USERNAME=europa

ENV USERNAME=${USERNAME}

# 패키지 설치
RUN apt update && \
    apt install --yes python3 python3-pip python3-venv curl wget zip fontconfig && \
    ln -fs /usr/share/zoneinfo/Asia/Seoul /etc/localtime

# D2Coding 설치
RUN mkdir -p /usr/share/fonts/truetype/d2coding && \
    wget https://github.com/naver/d2codingfont/releases/download/VER1.3.2/D2Coding-Ver1.3.2-20180524.zip -P /tmp && \
    unzip /tmp/D2Coding-Ver1.3.2-20180524.zip -d /usr/share/fonts/truetype/d2coding && \
    fc-cache -f -v

# 유저 등록
RUN useradd --base-dir /${USERNAME} \
            --home-dir /${USERNAME} \
            --create-home \
            --shell /bin/bash ${USERNAME}

# Jupyter Lab 설치
USER ${USERNAME}

RUN python3 -m venv ~/jupyter && \
    echo "source ~/jupyter/bin/activate" >> ~/.bashrc

RUN source /${USERNAME}/jupyter/bin/activate && \
    pip3 install jupyterlab jupyterlab-language-pack-ko-KR && \
    mkdir /${USERNAME}/.jupyter && \
    echo "c.ServerApp.ip = '*'" >> /${USERNAME}/.jupyter/jupyter_lab_config.py && \
    echo "c.PasswordIdentityProvider.hashed_password = '$(python -c "from jupyter_server.auth import passwd; print(passwd('${USERNAME}'))")'" >> /${USERNAME}/.jupyter/jupyter_lab_config.py && \
    echo "c.ServerApp.open_browser = False" >> /${USERNAME}/.jupyter/jupyter_lab_config.py

# 기본 설정
ARG SETTING_DIR=/${USERNAME}/.jupyter/lab/user-settings/@jupyterlab

RUN mkdir -p ${SETTING_DIR}/translation-extension/ && \
    echo '{ "locale": "ko_KR" }' > ${SETTING_DIR}/translation-extension/plugin.jupyterlab-settings && \
    mkdir -p ${SETTING_DIR}/apputils-extension/themes && \
    echo '{ "overrides": { "code-font-family": "D2Coding ligature", "code-font-size": "14px" } }' > ${SETTING_DIR}/apputils-extension/themes.jupyterlab-settings

# 마무리
RUN mkdir /${USERNAME}/workspace

WORKDIR /${USERNAME}/workspace

EXPOSE 8888/tcp

CMD ["bash", "-c", "source /${USERNAME}/jupyter/bin/activate && jupyter lab"]
