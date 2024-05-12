.. _reference-linux-fedora-centos-docker:

######
Docker
######

Fedora 40
=========

.. code-block:: bash

    sudo dnf remove docker \
        docker-client \
        docker-client-latest \
        docker-common \
        docker-latest \
        docker-latest-logrotate \
        docker-logrotate \
        docker-selinux \
        docker-engine-selinux \
        docker-engine

.. code-block:: bash

    sudo dnf -y install dnf-plugins-core
    sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo

.. code-block:: bash

    sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

.. code-block:: bash

    sudo groupadd docker
    sudo usermod -aG docker USERNAME

    sudo systemctl enable docker
    sudo systemctl start docker

.. code-block:: bash

    sudo firewall-cmd --permanent --zone=docker --change-interface=docker0
    sudo firewall-cmd --permanent --zone=trusted --add-interface=docker0
    sudo firewall-cmd --reload

Centos
======
.. code-block:: bash

    yum-config-manager \
        --add-repo \
        https://download.docker.com/linux/centos/docker-ce.repo

.. code-block:: bash

    dnf install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.6-3.3.el7.x86_64.rpm

.. code-block:: bash

    dnf install docker-ce docker-ce-cli containerd.io

.. code-block:: bash

    curl -L https://github.com/docker/compose/releases/download/1.25.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

.. code-block:: bash

    chmod +x /usr/local/bin/docker-compose
