FROM mcr.microsoft.com/devcontainers/miniconda:0-3

# Copy environment.yml (if found) to a temp location so we update the environment. Also
# copy "noop.txt" so the COPY instruction does not fail if no environment.yml exists.
COPY environment.yml* .devcontainer/noop.txt .devcontainer/conda_init.txt /tmp/conda-tmp/
RUN sudo apt-get update; \
    sudo apt-get -yq install vim
RUN conda install mamba -c conda-forge -y; \
    mamba install jupyterlab jupyterlab-git -c conda-forge -y; \
    if [ -f "/tmp/conda-tmp/environment.yml" ]; then umask 0002 && mamba env update -n base -f /tmp/conda-tmp/environment.yml; fi \
    && cat /tmp/conda-tmp/conda_init.txt >> /home/vscode/.bashrc \
    && sudo rm -rf /tmp/conda-tmp

# Install Julia and Julia kernel
RUN sudo wget https://julialang-s3.julialang.org/bin/linux/x64/1.8/julia-1.8.5-linux-x86_64.tar.gz; \
    sudo tar -xvzf julia-1.8.5-linux-x86_64.tar.gz; \
    sudo cp -r julia-1.8.5 /opt/; \
    sudo ln -s /opt/julia-1.8.5/bin/julia /usr/local/bin/julia
