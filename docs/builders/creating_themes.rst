创建主题
###############

:xref:`MJML` 使营销人员能够轻松地创建和维护美观且响应式的 Mautic 主题。

.. vale off

为什么要使用邮件主题？
*********************

主题的目的
==================

.. vale on

GrapesJS 构建器可以在"所见即所得"（WYSIWYG）环境中插入 HTML 代码并进行编辑。

主题可以包含各种预定义的区块和区域，反映所需的邮件设计——一个用于开始工作的模板。

通过选择主题，您可以非常高效地创建精美的邮件。

.. vale off

修改旧版主题
=======================

.. vale on

GrapesJS 构建器在列出可用主题之前会检查主题配置文件，以确定哪些主题与构建器兼容。

从 :xref:`Mautic 3` 开始，新增一行来定义兼容的构建器：

文件名：config.json

.. code-block:: json

    {
        "name": "Great Theme",
        "author": "Mr. Robot",
        "authorUrl": "https://mautic.org",
        "builder": "grapesjsbuilder",
        "features": [
            "email"
        ]
    }

定义构建器后，主题会显示在主题选择页面中。

如果您希望支持多个构建器，请以数组形式指定它们：``"builder": ["legacy", "grapesjsbuilder"],``

.. vale off

从头创建主题
*****************************

.. vale on

HTML 标记
===========

可以使用 HTML 来创建主题，GrapesJS 构建器提供基本的所见即所得编辑功能。

然而，一旦转换为 HTML，结构就变成了基于表格的，区块很难移动。因此，MJML 主题更为推荐。

MJML 标记
===========

MJML 语言允许创建可以在编辑器中自由移动的区块，无需编码即可从根本上改变布局。

为了充分利用 MJML 的功能，您必须用 MJML 编写整个主题。

最好的编写位置是 :xref:`MJML` 的在线编辑器。

有关使用区域、列和区块的文档，请参阅 :xref:`MJML Documentation`

.. vale off

头部组件
===============

.. vale on

Mautic 处理 ``<mj-head>`` 组件，包括 ``<mj-attributes>``。

通过 ``<mj-attributes>``，您可以为构建器区块定义默认样式。当您将区块拖入邮件编辑器时，它们会继承主题的颜色、字体和间距，而不是通用默认值。Brienz 主题展示了这种方法。

**已测试的元素** 包括：``mj-attributes``、``mj-breakpoint``、``mj-font``、``mj-html-attributes``、``mj-style``、``mj-title`` 和 ``mj-preview``。

.. vale off

正文组件
===============

.. vale on

目前，Mautic 处理大多数 ``<mj-body>`` 组件。

**已测试的元素** 有：mj-button、mj-column、mj-divider、mj-image、mj-navbar、mj-section、mj-spacer、mj-text

.. vale off

图片资源的相对 URL
=========================

.. vale on

图片必须按以下方式引用主题文件夹：

``<mj-image src="{{ getAssetUrl('Themes/'~Theme~'/assets/imagename.ext', null, null, true) }}" alt="logo" align="center" width="105px" padding="10px 0"></mj-image>``

文件结构

.. code-block::

    name.zip
    ├── assets
    │   ├── image1.ext
    │   └── image2.ext
    ├── html
    │   ├── email.html.twig
    │   ├── email.mjml.twig
    │   ├── base.html.twig
    │   └── message.html.twig
    ├── config.json
    └── thumbnail.png

保存主题包的步骤
===============================

在 MJML 中完成设计后，按以下步骤创建主题包：

* 将您的图片保存在 assets 文件夹中。

* 将您的 MJML 文件保存到 ``html`` 文件夹中，命名为 ``email.mjml.twig`` **和** ``email.html.twig``。

* 使用基本主题中的 ``base.html.twig`` 和 ``message.html.twig`` 文件，或在该处进行您的更改。

* 按上述说明保存您的 ``config.json``

* 创建缩略图——使用 400px 宽、600px 高的尺寸。

* 将文件夹内容压缩为 Zip 文件——确保文件和文件夹不在 Zip 文件的子文件夹中。