# agora-vai


 setSshCmd
        local PASSWORD=$(perl -e'print crypt("komodo", "aa")')
        local _UID=$(id -u ${USERNAME})
        ${SSH_CMD_ROOT} "useradd -d /komodo -u ${_UID} -g 100 -p ${PASSWORD} -s /bin/bash komodo && \
                        usermod -a -G sudo komodo && \
                        cp -R /root/.ssh /komodo/.ssh && \
                        chown ${_UID}:100 /komodo && chown -R ${_UID}:100 /komodo/.ssh && \
                        echo \"PATH=/komodo/dev/util/black:\$PATH\" >> /komodo/.profile && \
                        echo \"include \\\"/usr/share/themes/Radiance/gtk-2.0/gtkrc\\\"\" > /komodo/.gtkrc-2.0 && \
                        chown ${_UID}:100 /komodo/.profile && chown ${_UID}:100 /komodo/.gtkrc-2.0"
        ${CONTAINER_CMD} "useradd -d ${REALHOME} -u ${_UID} -g 100 -p ${PASSWORD} -s /bin/bash ${USERNAME} && \
                        usermod -a -G sudo ${USERNAME} && \
                        chown ${_UID}:100 ${REALHOME} && chown -R ${_UID}:100 ${REALHOME}/.komodo-dev && \
                        cp -R /root/.ssh ${REALHOME}/.ssh && chown -R ${_UID}:100 ${REALHOME}/.ssh && \
                        echo \"PATH=${KOPATH}/util/black:/opt/ActivePerl/site/bin:/opt/ActivePerl/bin:\\\$PATH\" >> ${REALHOME}/.bash_profile && \
                        chown ${_UID}:100 ${REALHOME}/.bash_profile"

    fi

