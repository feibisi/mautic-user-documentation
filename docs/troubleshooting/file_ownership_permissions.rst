文件所有权和权限
##############################

如果您遇到类似以下的错误：

.. code:: bash

    .WARNING: PHP Warning - require(/mautic/var/cache/prod/doctrine/orm/Proxies/__CG__MauticCategoryBundleEntityCategory.php): failed to open stream: No such file or directory - in file /mautic/vendor/doctrine/common/lib/Doctrine/Common/Proxy/AbstractProxyFactory.php - at line 209

很有可能是您的 Mautic 实例上的文件和文件夹的权限和/或所有权存在问题。

本文从使用 Apache 的 Linux 服务器的角度编写，这是 Mautic 最常见的托管环境。NGINX 和 IIS 服务器有不同的配置，但原理保持不变。

为什么权限很重要？
******************************

文件和文件夹权限指定了谁以及什么可以读取、写入、修改和访问它们。所有权决定了哪个用户"拥有"这些文件和文件夹——因此能够根据权限设置来执行操作。

用户
====

用户是文件的所有者。默认情况下，创建文件的人成为其所有者。因此，用户有时也被称为 **所有者**。

组
=====

一个组可以包含多个用户。属于某个组的所有用户对文件具有相同的访问权限。组简化了权限管理——特定组中的所有用户继承分配给该组的权限，而不是必须逐个为每个用户分配权限。

其他
=====

任何有权访问文件的其他用户都属于"其他"，这意味着他们既没有创建该文件，也不属于拥有该文件的组。实际上，这意味着"世界上的其他人"。因此，这也被称为 **面向世界的权限**。

Linux 区分这三种用户类型，以防止用户访问、编辑或删除他们不应更改的文件。阅读更多关于 :xref:`Linux file and folder ownership documentation` 的信息。

权限和所有权设置对于确保您的服务器和 Mautic 实例的安全性至关重要，因此正确设置非常重要。如果您的文件没有适当的权限，黑客更容易入侵您的文件并获取您 Mautic 实例的访问权限。正确设置文件权限可能不能让您免受所有攻击，但它有助于使您的 Mautic 实例更安全一些。

为什么权限问题会导致 Mautic 出错？
***************************************************

Mautic 需要在 Mautic 目录中读取和写入文件，以启用某些功能和脚本运行。如果权限设置不正确，或者运行这些功能的用户没有正确的访问权限，Mautic 将无法正常运行，结果会在应用和服务器日志中出现错误。

权限和所有权问题通常发生的原因是：

* 您以与 Mautic 运行所用用户不同的用户上传了 Mautic 或对文件和文件夹进行了更改——例如，您使用用户名为 ``bob`` 的 FTP 账户上传了文件，但您的 Web 服务器以名为 ``www-data`` 的用户执行脚本
* Mautic 运行所用的用户对文件和文件夹没有适当的权限——例如，``bob`` 无法创建目录或读取文件
* 您以与 Mautic 运行所用用户不同的用户运行了更新——导致某些文件和文件夹的所有权发生更改

如何修复 Mautic 中与权限相关的问题
************************************************

重置文件和文件夹的权限需要在命令行运行一些命令。您需要有服务器的 SSH 访问权限，或者请有权限的人为您执行这些命令。如果权限问题持续困扰您，某些托管提供商可能能够创建一个脚本来定期重置权限。

提供 cPanel 访问的托管提供商解决方案
=======================================================

一个用于修复 cPanel 账户上文件和目录权限和所有权的脚本。您可以要求您的托管提供商运行该脚本将权限重置为正确的值。在此处找到这个方便的脚本：:xref:`cPanel fix permissions script`。

识别问题
=======================

使用 SSH 登录您的服务器，并使用以下命令切换到 Mautic 目录：

.. code:: bash

    cd path/to/mautic

在此目录中，执行以下命令：

.. code:: bash

    ls -l

``ls`` 命令列出文件和目录。它有一个 ``-l`` 选项，以长格式列出内容，包括其权限和所有权及其他信息。

有关所有信息含义的更详细解释，请查看此文章：:xref:`Linux ls command`。

关键信息在第一列、第三列和第四列——权限以及拥有文件/文件夹的用户和组。

重置文件和文件夹权限
=====================================

如果您的文件和文件夹权限不正确，您可以运行以下命令来重置它们：

.. code-block:: bash

    find . -type f -not -perm 644 -exec chmod 644 {} +
    find . -type d -not -perm 755 -exec chmod 755 {} +
    chmod -R g+w var/cache/ var/logs/ app/config/
    chmod -R g+w media/files/ media/images/ translations/
    rm -rf var/cache/*

更改文件和文件夹的所有权
=====================================

即使文件和文件夹权限正确，如果您的文件和文件夹的所有权存在问题，错误仍然可能继续存在。这是因为用户可能没有必要的权限——因为他们不是文件/文件夹的所有者。阅读更多关于 :xref:`Linux file and folder ownership documentation` 的信息。

要找出 Apache 正在以哪个用户运行，请运行以下命令并记下返回行中的第一个条目：

.. code:: bash

    ps aux | grep apache2

使用此信息通过以下命令查找组：

.. code:: bash

    groups apache_user - 其中 apache_user 是您从上面第一步确定的用户

要重置文件和文件夹的所有权，请使用以下命令——确保将 ``apache_user`` 和 ``apache_group`` 替换为前面步骤中确定的值：

.. code:: bash

    sudo chown -R apache_user:apache_group /path/to/mautic

.. vale off

此命令 **ch-** anges **own-** ership（更改所有权），使用 ``-R`` 标志表示递归——包括该位置内的所有文件/文件夹。阅读更多关于 :xref:`Linux chown command` 的信息。

.. vale on
