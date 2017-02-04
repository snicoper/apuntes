.. _reference-linux-fedora-centos-reinstall_grup_post_install_windows:

###########################################
Reinstalar GRUB después de instalar windows
###########################################

**Fuentes:**

* http://www.supergrubdisk.org/super-grub2-disk/
* https://ask.fedoraproject.org/en/question/60906/problem-reinstalling-grub2-fedora-21/

Super Grub2 Disk
================

Con `Super Grub2 Disk <http://www.supergrubdisk.org/super-grub2-disk/>`_

Con la LIVE de Fedora
=====================

.. code-block:: bash

	sudo fdisk -l # Ver partición donde esta linux.

	sudo mount /dev/sda6 /mnt

	sudo mount --bind /dev /mnt/dev &&
	sudo mount --bind /dev/pts /mnt/dev/pts &&
	sudo mount --bind /proc /mnt/proc &&
	sudo mount --bind /sys /mnt/sys

	sudo chroot /mnt

	# sudo grub2-mkconfig -o /boot/grub2/grub.cfg ; #if needed
	sudo grub2-install /dev/sda ;#taking sda as the sata disk
