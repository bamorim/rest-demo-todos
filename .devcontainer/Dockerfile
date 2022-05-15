FROM hexpm/elixir:1.13.3-erlang-24.3.4-alpine-3.14.5
RUN apk add --no-cache git zsh starship shadow sudo nodejs npm make
RUN npm install -g apib2swagger

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME -s /bin/zsh \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
COPY zshrc /home/vscode/.zshrc
USER $USERNAME

RUN mix local.rebar --force && mix local.hex --force