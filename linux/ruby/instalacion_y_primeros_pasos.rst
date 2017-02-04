.. _reference-linux-ruby-instalacion_y_primeros_pasos:

################
Instalación Ruby
################

Instalación
***********

Dependencias para Ruby, si se omiten, cuando se instale Ruby desde rvm, pedirá instalarlas.

Requisitos
**********

.. code-block:: bash

    # Fedora
    sudo dnf install gcc-c++ patch readline readline-devel zlib zlib-devel \
        libyaml-devel libffi-devel openssl-devel make \
        bzip2 autoconf automake libtool bison sqlite-devel

    # Ubuntu
    sudo apt-get install gawk libreadline6-dev libyaml-dev libsqlite3-dev sqlite3 \
        autoconf libgdbm-dev libncurses5-dev automake libtool bison libffi-dev

    sudo apt-get install nodejs

rvm
***

.. code-block:: bash

    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

    \curl -sSL https://get.rvm.io | bash

.. code-block:: bash

    source ~/.profile

Ruby
****

Instalar Ruby **Tarda su tiempo!!**

.. code-block:: bash

    rvm install ruby
    ruby -v

Rails
*****

Instalar Rails

.. code-block:: bash

    gem install rails
    rails -v

SASS
****

.. code-block:: bash

    gem install sass
    sass -v
