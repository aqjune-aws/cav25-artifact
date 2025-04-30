FROM ubuntu:24.04

WORKDIR /cav25

RUN apt update
# HOL Light and OPAM dependencies
RUN apt -y install libpcre2-dev ocaml libstring-shellquote-perl libgmp-dev xdot make unzip
# Editor and cloc
RUN apt -y install cloc vim emacs
# Other utils
RUN apt -y install wget git

RUN git clone https://github.com/jrh13/hol-light.git && cd hol-light && git checkout c5e165f
RUN git clone https://github.com/awslabs/s2n-bignum.git && cd s2n-bignum && git checkout 1fcb664

# Install OPAM
RUN wget https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh
RUN mv install.sh opam-install.sh
RUN chmod +x opam-install.sh
RUN echo "/usr/local/bin" | sh ./opam-install.sh
RUN opam init --disable-sandboxing

# Build HOL Light
RUN apt -y install m4 pkg-config bzip2
RUN cd hol-light && make switch-5 && eval $(opam env) && HOLLIGHT_USE_MODULE=1 make
RUN echo 'export HOLDIR=/cav25/hol-light' >> ~/.bashrc

# Copy the patch
COPY s2n-bignum.patch s2n-bignum.patch
RUN cd s2n-bignum && git apply ../s2n-bignum.patch

ENTRYPOINT bash
