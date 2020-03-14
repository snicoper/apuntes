.. _reference-linux-fedora-centos-docker:

######
Docker
######

.. code-block:: bash

    sudo dnf config-manager \
        --add-repo \
        https://download.docker.com/linux/fedora/docker-ce.repo

    sudo dnf install docker-ce docker-ce-cli containerd.io

    sudo systemctl enable docker
    sudo systemctl start docker

    sudo groupadd docker
    sudo usermod -aG docker USERNAME
