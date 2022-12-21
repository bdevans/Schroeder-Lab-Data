# See here for image contents: https://hub.docker.com/r/jupyter/datascience-notebook/

# FROM jupyter/datascience-notebook
# FROM jupyter/scipy-notebook
FROM jupyter/minimal-notebook

# We want to run common-debian.sh from here:
# https://github.com/microsoft/vscode-dev-containers/tree/main/script-library#development-container-scripts
# But that script assumes that the main non-root user (in this case jovyan)
# is in a group with the same name (in this case jovyan).  So we must first make that so.
# COPY library-scripts/common-debian.sh /tmp/library-scripts/
USER root
# RUN apt-get update \
#  && groupadd jovyan \
#  && usermod -g jovyan -a -G users jovyan \
#  && bash /tmp/library-scripts/common-debian.sh \
#  && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts

# Install Python 3 packages
RUN mamba install --quiet --yes \
    # 'altair' \
    # 'beautifulsoup4' \
    # 'bokeh' \
    # 'bottleneck' \
    # 'cloudpickle' \
    # 'conda-forge::blas=*=openblas' \
    # 'cython' \
    # 'dask' \
    # 'dill' \
    # 'h5py' \
    # 'ipympl'\
    # 'ipywidgets' \
    # 'matplotlib-base' \
    # 'numba' \
    # 'numexpr' \
    # 'openpyxl' \
    # 'pandas' \
    # 'patsy' \
    # 'protobuf' \
    # 'pytables' \
    'scikit-image' && \
    # 'scikit-learn' \
    # 'scipy' \
    # 'seaborn' \
    # 'sqlalchemy' \
    # 'statsmodels' \
    # 'sympy' \
    # 'widgetsnbextension'\
    # 'xlrd' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# [Optional] If your pip requirements rarely change, uncomment this section to add them to the image.
COPY requirements.txt /tmp/pip-tmp/
RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
   && rm -rf /tmp/pip-tmp

# COPY --chown=${NB_UID}:${NB_GID} requirements.txt /tmp/
# RUN mamba install --yes --file /tmp/requirements.txt && \
#     mamba clean --all -f -y && \
#     fix-permissions "${CONDA_DIR}" && \
#     fix-permissions "/home/${NB_USER}"

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

USER jovyan