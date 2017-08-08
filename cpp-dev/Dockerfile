# arch linux development environment
from base/devel:latest
maintainer tsureshkumar@gmail.com
#change name here or pass through --build-args
ARG USERNAME=tsureshkumar 

RUN curl -o /etc/pacman.d/mirrorlist "https://www.archlinux.org/mirrorlist/?country=SG&protocol=https&ip_version=4&use_mirror_status=on" && sed -i 's/^#//' /etc/pacman.d/mirrorlist


RUN touch /root/.gnupg/dirmngr_ldapservers.conf \
 && pacman-key --refresh-keys && \
  pacman --sync --refresh --noconfirm --noprogressbar --quiet && \
    pacman --sync --noconfirm --noprogressbar --quiet archlinux-keyring openssl pacman && \
      pacman-db-upgrade && \
        pacman --sync --sysupgrade --noconfirm --noprogressbar --quiet && \
	  pacman --sync --noconfirm --noprogressbar --quiet git namcap pkgbuild-introspection \
	  emacs

#RUN git clone https://github.com/tsureshkumar/notebook.git
RUN useradd -ms /bin/bash $USERNAME && (echo -n "$USERNAME:passwd" | chpasswd) && groupadd sudo && (usermod -a -G sudo $USERNAME) && sed -i -e 's/# %sudo/%sudo/g' /etc/sudoers
RUN echo -n "root:toor" | chpasswd
USER $USERNAME
RUN mkdir ~/my && \
    cd ~/my && \
    git clone https://github.com/tsureshkumar/notebook.git && \
    (echo '.  ~/my/notebook/dots/dot-bash-rc' >> ~/.bash_profile) && \
    ln -s ~/my/notebook/dots/dot-vimrc ~/.vimrc && \
    (mkdir ~/.vim || :) && \
    mkdir -p ~/.vim && ln -s ~/my/notebook/dots/dot-vim-ycm_extra_conf.py ~/.vim/.ycm_extra_conf.py && \
    mkdir -p ~/.emacs.d/ && ln -s ~/my/notebook/emacs/init2.el ~/.emacs.d/init.el

WORKDIR /work
ENTRYPOINT ["bash"]
