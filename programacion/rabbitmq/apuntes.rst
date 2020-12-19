.. _reference-programacion-apuntes:

################
Apuntes RabbitMQ
################

Inicializar docker

.. code-block:: bash

    podman run -d \
    --hostname my-rabbit \
    --name some-rabbit \
    -e RABBITMQ_DEFAULT_USER=snicoper \
    -e RABBITMQ_DEFAULT_PASS=123456 \
    -p 4369:4369 \
    -p 5671:5671 \
    -p 5672:5672 \
    -p 25672:25672 \
    -p 15671:15671 \
    -p 15672:15672 \
    rabbitmq:3-management
