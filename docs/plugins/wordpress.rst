WordPress
#########

安装与激活
*************************

要求
============

- WordPress 4.6 或更高版本
- PHP 5.6 或更高版本

步骤
-----

1. 下载 WP Mautic 插件。
2. 前往您的 WordPress 管理仪表盘 → 插件 → 添加新插件。
3. 点击"上传插件"并选择下载的 ZIP 文件。
4. 点击"立即安装"，然后点击"激活"。

短代码与用法
********************

可用的短代码
====================

WP Mautic 目前通过 ``shortcodes.php`` 提供短代码 API。

示例用法
-------------

.. code-block:: php

   [mautic type="form" id="1"]

参数
==========

- **type:** Mautic 资源类型 - 例如 ``form``。
- **id:** 您要嵌入的 Mautic 表单或资源的 ID。

跟踪脚本行为
************************

.. vale off

页头 vs 页脚
====================
您可以选择在站点页头加载 Mautic 跟踪脚本 - 以便更快地进行页面浏览跟踪 - 或在页脚加载 - 以获得更好的性能。

.. vale on

回退跟踪
=================

如果访问者关闭了 JavaScript，系统会自动添加一个回退的 ``<img>`` 标签，通过跟踪像素进行跟踪。

自定义属性
=================

.. vale off

插件会自动发送额外的元数据，如语言、页面标题、引荐来源以及用户详情（如果启用）。

.. vale on

插件设置
***************

访问设置
======================

从您的 WordPress 仪表盘导航到 **设置 → WPMautic**。

可用选项
=================

.. vale off

- **基础 URL:** 您的 Mautic 实例的 URL - 例如 ``https://example.mautic.com``。
- **脚本位置:** 选择在页头、页脚注入跟踪代码，或关闭它。
- **跟踪已登录用户:** 启用对已登录用户的详细信息跟踪，如邮件、用户名。
- **回退激活:** 如果您关闭 JavaScript，添加 ``<noscript>`` 图片跟踪回退。

.. vale on

开发者
**********

本节涵盖设置环境以及与 WordPress 集成所需了解的所有内容。

环境
===========

在开始开发之前，请确保您的系统上已运行 **Docker**。

入门
---------------

首先，克隆 WordPress 开发仓库：

.. code-block:: bash

  git clone https://github.com/WordPress/wordpress-develop.git

进入克隆的目录：

.. code-block:: bash

  cd wordpress-develop

初始设置
-------------

运行以下命令来设置您的环境：

.. code-block:: bash

  npm install
  npm run build:dev
  npm run env:start
  npm run env:install

这些命令：

.. vale off

- 安装所有 Node.js 依赖项。
- 构建 WordPress 资源的开发版本。
- 启动 WordPress 的本地 Docker 容器。
- 将 WordPress 安装到 Docker 环境中。

.. vale on

实用命令
---------------

设置完成后，您可以使用以下命令来控制您的环境：

- ``npm run env:start`` 启动 Docker 容器。
- ``npm run env:stop`` 停止 Docker 容器。
- ``npm run env:restart`` 重启 Docker 容器。

钩子与函数
===================

实用函数
----------------

- ``wpmautic_option( $option, $default )`` 安全地获取插件设置。
- ``wpmautic_base_script()`` 获取 ``mtc.js`` 脚本的完整 URL。
- ``wpmautic_get_tracking_attributes()`` 获取自定义跟踪数据数组。

过滤器
-------

使用以下方式扩展插件：

.. code-block:: php

  apply_filters('wpmautic_tracking_attributes', $attrs)

操作
-------

- ``wp_head`` 或 ``wp_footer`` 根据设置自动注入 Mautic 脚本。
