FROM archlinux:base-devel

ENV TZ=Asia/Shanghai

# basic
RUN yes | pacman -Syu
RUN yes | pacman -S git zsh which vim tree unzip gcc make tzdata
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo "export LANG=en_US.UTF-8" >> /etc/profile.d/locale.sh; \
    echo "export LC_ALL=en_US.UTF-8" >> /etc/profile.d/locale.sh; \
    echo "Asia/Shanghai" > /etc/timezone

# oh my zsh
RUN yes | sh -c "$(curl -fsSL https://ghproxy.com/https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
ENV SHELL /bin/zsh

# Go
RUN yes | pacman -S go
ENV GOPATH /root/go
ENV PATH $GOPATH/bin:$PATH
ENV GOROOT /usr/lib/go
RUN go env -w GO111MODULE=on &&\
    go env -w GOPROXY=https://goproxy.cn,direct &&\
		go install github.com/silenceper/gowatch@latest &&\
    go install golang.org/x/tools/gopls@latest

# Bun
RUN curl -fsSL https://bun.sh/install | bash
RUN exec /usr/bin/zsh

# others
RUN git config --global core.editor "code --wait"; \
    git config --global init.defaultBranch master; \
    git config --global user.name "Kalougata"; \
    git config --global user.email "kalougata@111.com"
