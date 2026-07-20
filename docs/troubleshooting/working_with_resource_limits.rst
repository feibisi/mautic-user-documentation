处理资源限制
############################

在安装或使用 Mautic 时，您可能会遇到服务器配置的限制。这些通常表现为以下错误：

.. code:: bash

    The Uploaded file exceeds the upload_max_filesize directive
    Maximum execution time of 30 seconds exceeded - in file <filepath> - at line <line number>
    PHP Error: Allowed memory size of <number> bytes exhausted (tried to allocate <number> bytes) - in file <filepath> - at line <number>

这些通常不是 Mautic 的错误，而是您的服务器配置问题。要解决这些问题，您需要对服务器配置进行一些更改。

解决问题
****************

要解决这些问题，您需要：

* 能够访问您的服务器以更改配置文件——通常通过 SSH——或；
* 能够访问您的托管提供商的控制面板，这可能允许您通过用户界面更改这些设置
* 能够使用文本编辑器，如 ``Nano`` 或 ``Vi``

.. note::
    注意：本教程中使用的是 Nano，如果您不使用 Nano，只需将 'nano' 替换为您偏好使用的编辑器名称。使用 Nano 时，请参阅此 :xref:`Nano keyboard commands` 速查表，获取有用的键盘快捷键指南。

找到已加载的 ``php.ini`` 文件
********************************

第一步是找到正在使用的 ``php.ini`` 文件。:xref:`php.ini file` 是一个控制 PHP 如何运行的配置文件。

您可以访问 Mautic
=========================

如果您可以访问 Mautic 实例，请导航至 设置 > 系统信息 > PHP 信息，您可以在其中查看一个文件，该文件告诉您 Mautic 正在使用的每个 PHP 配置设置。特别地，下面截图中红色标出的区域为您提供了相关文件的路径。

.. image:: images/phpini-settings.png
    :width: 400
    :alt: Screenshot of PHP settings in Mautic dashboard

关于本地值与主值的注意事项
------------------------------------

当您查看 PHP 信息文件时，有两个值，``Master`` 和 ``Local``。

主值
~~~~~~~~~~~~

这来自您的 ``php.ini`` 主文件——即前面部分中加载的那个文件。这是应用于整个服务器的值。

本地值
~~~~~~~~~~~

全局设置可以在多个位置被本地覆盖，如 ``httpd.conf``、``.htaccess`` 或其他 Apache 配置。

这通常用于绕过服务器级别的限制性设置，有时可能意味着在顶层全局级别所做的更改不会渗透到您的特定文件夹或位置。因此，如果您发现两个值之间存在差异，请在 Mautic 目录中查找本地的 ``.htaccess`` 或 ``*.ini`` 文件，或向您的托管提供商验证。

您无法访问 Mautic
===============================

如果您无法访问 Mautic 的系统信息，可以使用命令验证 ``php.ini`` 的路径：

.. code:: bash

    php -i | grep .ini

您也可以使用相同的命令来查找所使用的特定值：

.. code:: bash

    php -i | grep upload_max_filesize

其中 ``upload_max_filesize`` 是您需要更改的值。

更新值
------------------

一旦您找到了正在使用的 ``php.ini`` 文件，您应该能够使用以下命令编辑它：

.. code:: bash

    sudo nano path/to/file/php.ini

使用 ``ctrl+w``——"where" 的键盘快捷键——然后输入您需要更改的设置——例如 ``upload_max_filesize``，来找到相关设置。

更改您在 ``php.ini`` 文件中看到的值，然后保存，使用 ``ctrl+x``——"exit" 的键盘快捷键——然后按 ``y`` 保存更改。

.. vale off

重启 Apache
-----------------

.. vale on

保存更改后，您需要重启 Apache 以使更改生效。

最好先进行一次预演，使用 :xref:`Apache configtest` 命令

.. code:: bash

    sudo apachectl configtest

这会在重启服务之前检查您的 Apache 配置是否健全。在重启 Apache 之前解决任何识别出的问题。

一旦您满意，运行以下命令重启 Apache：

.. vale off

Ubuntu 和 Debian
~~~~~~~~~~~~~~~~~

.. vale on

.. code:: bash

    sudo systemctl restart apache2

.. vale off

CentOS 和 Red Hat
~~~~~~~~~~~~~~~~~~

.. vale on

.. code:: bash

    sudo systemctl restart httpd

覆盖值
--------------------

如果您无法在 ``php.ini`` 级别更改值，可能可以在本地文件夹级别覆盖该值——具体取决于您的服务器配置。

查看此 :xref:`PHP config changes` 文章，了解更多关于如何使用本地 ``.htaccess`` 文件覆盖 ``php.ini`` 设置的详细信息。

作为您可能希望在本地 htaccess 文件中用于覆盖全局 ``php.ini`` 文件中值的两个设置示例：

.. code:: bash

    php_value upload_max_filesize 20M
    php_value max_execution_time 600

这是最后的手段，您的托管提供商可能不支持。