UTM 标签
########

UTM 标签也称为参数或短文本代码。在 URL 或链接中添加这些标签后，营销人员可以跟踪效果、创建自定义受众群体，并分析来自不同来源的网站流量。营销人员还可以将 UTM 标签与 Google Analytics 一起使用，以清楚了解其营销内容的效果和营销项目的投资回报率。

使用 UTM 标签的主要好处
******************************

通过 UTM 标签，您可以：

- 跟踪营销项目的价值并衡量投资回报率
- 获取关于转化和流量来源的精确数据
- 通过 A/B 测试来测试营销内容的效果

在 Mautic 中使用 UTM 标签
************************

要将 UTM 标签与 Google Analytics 一起使用并使其显示在您的 Google Analytics 仪表盘中，您必须在您要链接到的资源上安装 Google Analytics 跟踪代码。这会与您的 Google Analytics 仪表盘同步并记录 UTM 标签。

如果您使用 Mautic 落地页，您必须前往 设置 > 配置 > 跟踪设置，并添加您的 Google Analytics ID。

  .. image:: images/utm_tags/add_google_analytics_id.png
    :alt: Screenshot showing the option to add your Google Analytics ID

如果您使用非 Mautic 落地页，您必须在第三方页面上手动嵌入 Google Analytics 跟踪脚本。

Mautic 用户可以在邮件或焦点项目中自动将 UTM 标签附加到所有链接。对于其他渠道，您可以通过在 URL 地址中包含 UTM 值来使链接可追踪。当联系人点击邮件或焦点项目中的链接时，Mautic 会记录 UTM 标签并将其存储在联系人记录中。您可以在联系人事件历史概览中找到详细信息。记录 UTM 标签后，您可以将其用作分组中的筛选器。

您可以使用 UTM 标签来跟踪从邮件中的动态网页内容插槽转化的联系人，并在 Google Analytics 或 Mautic 报告中确定来源。您还可以通过选择 UTM 代码作为数据源，将其用作报告中的列。

下表列出了 Google Analytics UTM 标签：

.. list-table:: 标题
   :widths: 50 50
   :header-rows: 1

   * - UTM 标签
     - 描述
   * - 营销活动来源
     - 网络活动的引荐来源。它表示引荐流量的社交网络、搜索引擎、新闻通讯名称或任何其他特定来源。
        * 示例：``facebook``、``twitter``、``blog``、``newsletters``
        * UTM 代码：``utm_source``
        * 示例代码：``utm_source=facebook``
   * - 营销活动媒介
     - UTM 标签 - Mautic 文档
         * 示例：``cpc``、``organic_social``
         * UTM 代码：``utm_medium``
         * 示例代码：``utm_medium=paid_social``
   * - 营销活动名称
     - 您想要跟踪的特定促销或营销活动标题。
         * 示例：``summer_sale``、``free_trial``
         * UTM 代码：``utm_campaign``
         * 示例代码：``utm_campaign=summer_sale``
   * - 营销活动内容
     - 消息中的资源。此不可配置的值会自动填充与特定资源关联的内容资源标识符。
   * - 营销活动关键词
     - 搜索营销活动的关键词。此不可配置的值会自动填充在链接文字中，并跟踪消息中的链接。

.. note::
    您不需要填写所有选项。您可以根据需要使用一个、几个或全部选项。

.. vale off

在邮件中使用 UTM 标签
************************

.. vale on

Mautic 支持在邮件中使用 UTM 标记。Mautic 可以通过在提供的字段中输入相应的营销活动值，自动将 UTM 标签附加到邮件中的所有链接。

#. 在 Mautic 中，点击 渠道 > 邮件。
#. 创建新邮件或编辑现有邮件。如果选择编辑现有邮件，请点击该邮件然后点击编辑。
#. 找到右下方的 Google Analytics UTM 标签部分。
#. 在字段中输入相应的信息。
#. 点击应用。

.. warning::
    * 在邮件中添加链接时，请使用构建器中的编辑链接图标。
    * 在代码模式下添加链接时，请使用 <a href> 标签。
    * 所有链接必须包含尾部斜杠。否则，UTM 代码不会被附加。

在焦点项目中使用 UTM 标签
*****************************

Mautic 支持在 :doc:`/channels/focus_items` 中使用 UTM 标记。Mautic 可以通过在提供的字段中输入相应的值，自动将 UTM 标签附加到焦点项目中的所有链接。

#. 点击 渠道 > 焦点项目
#. 创建新的焦点项目或打开现有的焦点项目。
#. 找到右下方的 Google Analytics UTM 标签部分。
#. 在字段中输入相应的信息。
#. 点击应用。