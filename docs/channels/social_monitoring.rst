.. vale off

社交监测
#################

.. vale on

可以通过监测 Twitter 的提及和话题标签来将联系人添加到 Mautic 中。

要求
************

- 您必须先配置 :doc:`/plugins/twitter` 插件
- 您必须定期触发社交监测 :doc:`定时任务 </configuration/cron_jobs>`。

.. vale off

创建社交监测
*************************

.. vale on

要创建新的社交监测，请前往 渠道 > 社交监测 并点击新建。

Mautic 在创建社交监测时提供了两个选项：

- **Twitter 提及** — 每当有人提及指定用户名时，Mautic 会将其创建为联系人
- **Twitter 话题标签** — 每当有人在推文中使用指定的话题标签时，Mautic 会将其创建为联系人。

  .. image:: images/social_monitoring/social_monitor.jpeg
    :width: 400
    :alt: Screenshot showing the creation of a new Social Monitor.

社交提及
===============

选择 Twitter 提及监测方式时，可使用以下字段：

- **Twitter 提及** — 您想要跟踪提及的 Twitter 用户名。不要包含 @ 符号——例如 ``mauticcommunity``。
- **描述** — 在 Mautic 内部使用的描述，用于告知营销人员此监测正在跟踪什么。
- **匹配联系人姓名** — 如果设置为"是"，Mautic 会尝试匹配从 Twitter 创建的联系人姓名，并将 Twitter 账户与其现有的联系人记录关联起来。如果设置为"否"，则不会发生此操作，您可能会遇到联系人重复的问题。

还提供标准的 Mautic 字段：

**活动** — 这允许您设置社交监测的激活状态。停用的社交监测不会收集新的联系人。

.. vale off

**激活时间（日期/时间）** — 这允许您定义此社交监测开始监测新联系人的日期和时间。例如，您可以使用它来与某个活动的时间相配合。

**停用时间（日期/时间）** — 这允许您定义此社交监测停止监测新联系人的日期和时间。

.. vale on

**联系人分组** — 这允许您定义在 Mautic 中通过此社交监测检测到的联系人加入的分组。这对于识别正在讨论您品牌的人非常有用，可直接将他们添加到分组中以采取进一步行动。

  .. image:: images/social_monitoring/social_monitoring_mentions.png
    :width: 400
    :alt: Screenshot showing the creation of a new Twitter Mentions Social Monitor.

话题标签
========

选择 Twitter 话题标签监测方式时，可使用以下字段：

- **Twitter 话题标签** — 您想要跟踪的 Twitter 话题标签提及。不要包含 # 符号——例如 ``mautic``。
- **描述** — 在 Mautic 内部使用的描述，用于告知营销人员此监测正在跟踪什么。
- **匹配联系人姓名** — 如果设置为"是"，Mautic 会尝试匹配从 Twitter 创建的联系人姓名，并将 Twitter 账户与其现有的联系人记录关联起来。如果设置为"否"，则不会发生此操作，您可能会遇到联系人重复的问题。

还提供标准的 Mautic 字段：

**活动** — 这允许您设置社交监测的激活状态。停用的社交监测不会收集新的联系人。

.. vale off

**激活时间（日期/时间）** — 这允许您定义此社交监测开始监测新联系人的日期和时间。例如，可以使用它来与某个活动的时间相配合。

**停用时间（日期/时间）** — 这允许您定义此社交监测停止监测新联系人的日期和时间。

.. vale on

**联系人分组** — 这允许您定义在 Mautic 中通过此社交监测检测到的联系人加入的分组。这对于识别正在讨论您品牌的人非常有用，可直接将他们添加到分组中以采取进一步行动。

  .. image:: images/social_monitoring/social_monitoring_hashtags.png
    :width: 400
    :alt: Screenshot showing the creation of a new Twitter Hashtags Social Monitor.