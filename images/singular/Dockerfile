FROM jupyter/minimal-notebook@sha256:31c4e330d97bc475666968edda0967c4007345aafae8c876634d66bf5c7ac1bb

COPY environment.yml /tmp/environment.yml
RUN conda env update -n root --file /tmp/environment.yml \
 && conda clean -pity \
 && jupyter lab build \
 && jupyter lab clean

RUN pip install -v --no-cache pysingular jupyter_kernel_singular

USER root

ENV HOME=/home/user
RUN mkdir $HOME \
 && chown $NB_USER $HOME \
 && usermod -d $HOME $NB_USER

USER $NB_USER

ADD entrypoint /usr/local/bin/entrypoint
ENTRYPOINT ["/usr/local/bin/entrypoint"]

WORKDIR $HOME
