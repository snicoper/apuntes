.. _reference-linux-fedora-centos-docker:

######
Docker
######

.. code-block:: bash

    sudo dnf config-manager \
        --add-repo \
        https://download.docker.com/linux/fedora/docker-ce.repo

    sudo dnf install docker-ce docker-ce-cli containerd.io docker-compose

.. code-block:: bash

    sudo groupadd docker
    sudo usermod -aG docker USERNAME

    sudo systemctl enable docker
    sudo systemctl start docker

.. code-block:: bash

    sudo firewall-cmd --permanent --zone=trusted --add-interface=docker0
