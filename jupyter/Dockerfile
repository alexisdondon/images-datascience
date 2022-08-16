ARG BASE_IMAGE=jupyter/python:latest
FROM $BASE_IMAGE

SHELL ["/bin/bash", "-c"]

USER ${USERNAME}

RUN mamba install -y -c conda-forge \
        ipywidgets \
        jupyterlab \
<<<<<<< HEAD
        jupyterlab-git
    # Fix permissions
    #chown -R ${USERNAME}:${GROUPNAME} ${HOME} && \
    # Clean 
    #mamba clean --all -f -y && \
    #jupyter lab clean
=======
        jupyterlab-git && \
    # Make Julia kernel available in Jupyter
    julia -e 'using Pkg; pkg"add IJulia"; pkg"precompile"' && \
    mv "${HOME}/.local/share/jupyter/kernels/julia"* "${MAMBA_DIR}/share/jupyter/kernels/" && \
    # Fix permissions
    chown -R ${USERNAME}:${GROUPNAME} ${HOME} ${MAMBA_DIR} && \
    # Clean 
    rm -rf "${HOME}/.local" && \
    mamba clean --all -f -y && \
    jupyter lab clean
>>>>>>> 0a3b76245e387c14cae7e1950e2ffb733abde599

COPY start-onyxia.sh /usr/local/bin/
EXPOSE 8888

CMD ["jupyter", "lab", "--no-browser", "--ip '0.0.0.0'"]
