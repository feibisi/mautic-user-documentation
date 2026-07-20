.. vale off

如何切换到 Composer
#########################

.. vale on

在 Mautic 4 之前，您可以将 Mautic 下载为 ZIP 文件并安装在任何 PHP 服务器上。

然而，许多 Mautic 用户在安装和更新过程中遇到错误，其中不少错误导致了相当大的困扰，在某些情况下甚至造成了严重的业务中断。

此外，Mautic 最近引入了 :ref:`Mautic 市场`，该功能与此安装方法不兼容。

.. vale off

由于上述原因，从 Mautic 5 发布开始，Composer 成为安装和更新 Mautic 的默认方法。更多信息请阅读 :xref:`composer blog post`。

.. vale on

切换到基于 Composer 的安装
******************************************

在开始之前，最好理解 Mautic 的两个方面：

* 数据库 - Mautic 存储您的联系人数据的地方。

* 代码库 - Mautic 与数据库交互的地方。

切换到基于 Composer 的安装时，**数据库**不会受到影响，只有**代码库**会发生变化。

在本教程中，假设 Mautic 当前安装在 ``/var/www/html`` 中。

以下是切换到基于 Composer 的安装所需的步骤：

#. 进入 ``/var/www``

#. 运行 ``composer create-project mautic/recommended-project:^5 html-new --no-interaction``

#. 将以下文件和文件夹从 ``/var/www/html`` 复制到 ``/var/www/html-new``：

   * 配置文件 - 通常位于 ``app/config/local.php`` - 移动到 ``docroot/app/config/local.php``

   * 整个 ``plugins`` 目录 - 移动到 ``docroot/plugins``。
 
   * 上传文件 - 通常位于 ``app/media/files`` 和 ``app/media/images`` - 分别移动到 ``docroot/app/media/files`` 和 ``docroot/app/media/images``。

   * 来自 ``app/media/dashboards`` 的自定义仪表板 - 移动到 ``docroot/app/media/dashboards``
   
   * 来自 ``themes`` 的任何自定义主题 - 移动到 ``/docroot/themes``

   * 来自 ``translations`` 的任何翻译文件 - 移动到 ``/docroot/translations``

#. 将 ``/var/www/html`` 重命名为 ``/var/www/html-old``，并将 ``/var/www/html-new`` 重命名为 ``/var/www/html``

#. 更新您的 Web 服务器配置，使其指向 ``/var/www/html/docroot`` 而非 ``/var/www/html``

#. 登录 Mautic，在全局设置中启用切换以使用 Composer 完全管理 Mautic - 这也使您能够使用 Mautic 市场。

.. image:: images/switch-enable-composer.png
  :width: 600
  :alt: 启用 Composer 切换的截图

您已成功切换到基于 Composer 的安装。测试 Mautic 以确认其运行正常。

.. vale off

常见问题
**************************

问：现有数据会保留吗？

答：是的，切换到基于 Composer 的安装仅影响应用程序文件。它不会以任何方式影响您的数据。

问：切换到基于 Composer 的安装所需的最低 Mautic 版本是多少？

答：要切换到基于 Composer 的安装，至少需要 Mautic 4.0.0 版本。

.. vale on