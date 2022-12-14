FROM ubuntu:22.04

ARG UTLN
ARG COURSE_FOLDER

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y \
            lsb-release build-essential software-properties-common \
            wget git ssh sudo time \                                        
            clang-12 clang-format valgrind \
            python3-pip jq x11-apps

# install opengl / fltk (for graphics course)
# RUN apt-get install -y libglu1-mesa-dev freeglut3-dev mesa-common-dev libglew-dev 
# RUN apt-get install -y mesa-utils libgl1-mesa-glx fltk1.3-dev libglm-dev

# install python packages
RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install toml dataclasses tqdm filelock python_dateutil

# use clang++
RUN ln -s /usr/bin/clang++-12 /usr/bin/clang++

RUN adduser --disabled-password --gecos "" ${UTLN} 
RUN usermod -aG sudo ${UTLN}

RUN printf "${UTLN}  ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
RUN printf "export PS1=\"\\u@${COURSE_FOLDER}-local:\\W\\$ \"\n" >> /home/${UTLN}/.bashrc
RUN printf "export UTLN=${UTLN}\n" >> /home/${UTLN}/.bashrc
RUN printf "export COURSE_FOLDER=${COURSE_FOLDER}\n" >> /home/${UTLN}/.bashrc
RUN printf "export PATH=\${PATH}:/workspaces/${COURSE_FOLDER}/.devcontainer/scripts\n" >> /home/${UTLN}/.bashrc
