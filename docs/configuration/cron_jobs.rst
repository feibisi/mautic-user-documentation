.. vale off

定时任务
#########

.. vale on

.. attention::

    Mautic 3 引入了定时任务的新路径 ``bin/console`` - 如果您使用的是旧版 Mautic 2.x 系列，应将其替换为旧版本 ``app/console``

Mautic 需要一些 :xref:`cron jobs` 来处理维护任务，例如更新联系人或营销活动、执行营销活动操作、发送邮件等。
您必须手动将所需的定时任务添加到服务器。
大多数网络主机都提供通过 SSH、cPanel 或其他自定义面板添加定时任务的方式。
如果您不确定如何设置定时任务，请查阅主机的文档或联系技术支持。

如果您不熟悉 Linux 或定时任务，Apache 基金会提供了 :xref:`an excellent guide` ，建议您通过各技术支持渠道提问前先阅读。

设置定时任务时，您需要选择运行频率。许多共享主机倾向于每 15 或 30 分钟运行一次脚本，甚至可能为满足这些限制而覆盖预定时间。请查阅主机文档了解是否存在此类限制。

**强烈建议将以下必需任务错开执行时间，避免在同一分钟运行。**

例如：

.. code-block::

    - 0,15,30,45 <— mautic:segments:update
    - 5,20,35,50 <— mautic:campaigns:update
    - 10,25,40,55 <— mautic:campaigns:trigger

必需任务
********

Mautic 需要按以下方式定期运行一些强制性的定时任务：

分组定时任务
=================

**保持分组数据最新：**

.. code-block:: php

    php /path/to/mautic/bin/console mautic:segments:update

默认情况下，脚本每批处理 300 个联系人。如果对服务器资源而言数量过多，请使用 ``--batch-limit=X`` 选项，将 X 替换为每批处理的联系人数量。

您还可以使用 ``--max-contacts`` 限制每次脚本执行处理的联系人数量，以进一步控制资源使用。

.. vale off

营销活动定时任务
==================

.. vale on

**保持营销活动与适用的联系人同步更新：**

.. code-block:: php

    php /path/to/mautic/bin/console mautic:campaigns:update

默认情况下，脚本每批处理 300 个联系人。如果对服务器资源而言数量过多，请使用 ``--batch-limit=X`` 选项，将 X 替换为每批处理的联系人数量。

您还可以使用 ``--max-contacts`` 限制每次脚本执行处理的联系人数量，以进一步控制资源使用。

**执行营销活动事件：**

.. code-block:: php

    php /path/to/mautic/bin/console mautic:campaigns:trigger

默认情况下，脚本每批处理 100 个事件。如果对服务器资源而言数量过多，请使用 ``--batch-limit=X`` 选项，将 X 替换为每批处理的事件数量。

您还可以使用 ``--max-events`` 限制每次脚本执行处理的事件数量，以进一步控制资源使用。

自 Mautic 5.1 起，Mautic 按从最新到最旧的顺序触发营销活动。这样您就可以优先处理较新的营销活动。

.. vale off

**发送频率规则重新排期的营销活动消息：** 如果系统范围内或针对每个联系人设置了频率规则，标记为*营销消息*的消息（例如作为营销活动一部分的邮件）将被保留在消息队列中。要处理此队列并重新排期发送这些消息，请添加此定时任务：

.. vale on

``mautic:messages:send``

.. note::

    这些消息仅在系统范围内或针对每个联系人应用频率规则时才会被添加到队列中。

.. vale off

自定义字段定时任务
=======================

.. vale on

**保持联系人和公司自定义字段更新**

.. code-block:: php

    php /path/to/mautic/bin/console mautic:custom-field:create-column
    php /path/to/mautic/bin/console mautic:custom-field:delete-column

可选任务
********

根据您的服务器配置，您可以设置用于发送邮件、导入联系人等任务的可选定时任务。可选定时任务如下：

.. vale off

处理邮件队列定时任务
============================

.. vale on

如果系统配置将邮件加入队列，则定时任务会处理它们。如果您计划使用定时任务运行 ``messenger:consume``，则应至少包含以下参数之一：``--memory-limit``、``--limit``（邮件数量）或 ``--time-limit``。这将会启动一个长期运行的进程，如果没有这些参数，进程将持续运行。

.. code-block:: bash

    php /path/to/mautic/bin/console messenger:consume email --time-limit=160

.. vale off

获取并处理受监控邮件定时任务
==========================================

.. vale on

如果您使用退信管理，请设置以下命令来获取并处理消息：

.. code-block:: php

    php /path/to/mautic/bin/console mautic:email:fetch

.. vale off

社交监控定时任务
==========================

.. vale on

如果您使用社交监控，请将以下命令添加到您的定时任务配置中：

.. code-block:: php

    php /path/to/mautic/bin/console mautic:social:monitoring

.. vale off

导入联系人定时任务
========================

.. vale on

要在后台导入特别大量的联系人或者公司，请使用以下命令：

.. code-block:: php

    php /path/to/mautic/bin/console mautic:import

此命令的执行时间取决于 CSV 文件中的联系人数量。然而，导入操作成功完成后，Mautic 仪表盘上会出现一条通知。

.. vale off

导出联系人定时任务
========================

.. vale on

要导出联系人到 CSV 并通过邮件发送结果，请使用以下命令：

.. code-block:: bash

    php /path/to/mautic/bin/console mautic:contacts:scheduled_export

此命令的执行时间取决于 CSV 文件中的联系人数量。然而，导出操作成功完成后，Mautic 会发送一封包含 CSV 下载链接的邮件。

Webhooks 定时任务
=================

如果 Mautic 配置设置包含 Webhook 批处理，请使用以下命令发送负载：

.. code-block:: php

    php /path/to/mautic/bin/console mautic:webhooks:process

自 Mautic 5.1 起，还可以在“范围模式”下运行 Webhooks 定时任务。这允许您指定在单次运行中处理的 Webhook 事件范围。如果您有大量 Webhook 事件需要处理，并且希望避免内存耗尽，这会很有用。

要使用此模式，您可以指定 ``--min-id`` 和 ``--max-id`` 选项。例如，要处理 ID 为 5 的 Webhook 的事件，您可以指定只处理该 Webhook 中 ID 在 1000 到 2000 之间的事件，使用以下命令：

.. code-block:: bash

    bin/console mautic:webhooks:process --webhook-id=5 --min-id=1000 --max-id=2000

.. _cron jobs:

.. vale off

更新 MaxMind GeoLite2 IP 数据库定时任务
============================================

.. vale on

Mautic 默认使用 :xref:`MaxMind's` 的 GeoLite2 IP 数据库。
该数据库的许可证是 :xref:`Creative Commons Attribution-ShareAlike 3.0 Unported License`，因此 Mautic 无法将其包含在安装包中。
您可以通过 Mautic 的配置手动下载数据库，或者使用以下脚本自动下载。MaxMind 会在每个月的第一个星期二更新其数据库。

.. code-block:: php

    php /path/to/mautic/bin/console mautic:iplookup:download

清理旧数据定时任务
==========================

通过清除旧数据来清理 Mautic 安装。请注意，某些类型的数据无法在 Mautic 中清除。
目前支持清除的数据包括审计日志条目、访客（匿名联系人）以及访客着陆页点击。在进行任何更改之前，请使用 ``--dry-run`` 查看将受影响的记录数量。

使用 ``--gdpr`` 标志删除数据以符合 GDPR 欧盟法规。这将删除已处于非活动状态 3 年的联系人。

**此操作会永久删除数据。在酌情使用之前，请务必验证数据库备份。**

.. code-block:: php

    php /path/to/mautic/bin/console mautic:maintenance:cleanup --days-old=365 --dry-run

MaxMind CCPA 合规定时任务
================================

MaxMind 要求用户维护一个最新的“禁止出售”列表，并删除 MaxMind 中过去与此类 IP 地址相关的所有数据。

更多详情请参见官方 :xref:`MaxMind website`。

建议每周运行一次这两个命令，按顺序执行。

.. code-block:: php

    php /path/to/mautic/bin/console mautic:donotsell:download

此命令从 MaxMind 下载“禁止出售”IP 地址的数据库。

.. code-block:: php

    php /path/to/mautic/bin/console mautic:max-mind:purge

此命令查找数据库中从 MaxMind 的“禁止出售”IP 地址加载的数据，并删除这些数据。

.. vale off

发送预定的广播（分组邮件）定时任务
===================================================

.. vale on

从 Mautic 2.2.0 开始，可以使用 cron 来发送频道通信的预定广播。目前唯一实现此功能的是分组邮件。现在，无需手动发送并在浏览器窗口保持打开状态等待 AJAX 分批发送，您可以使用命令来启动该过程。

需要注意的是，邮件必须具有发布日期，并且当前处于已发布状态 - 这是为了防止任何无意的邮件广播。与手动/AJAX 过程一样，该消息仅发送给尚未收到特定通信的联系人。此命令会将消息发送给稍后添加到源分组的联系人，所以如果您不希望发生这种情况，请设置一个取消发布日期。

.. code-block:: php

    php /path/to/mautic/bin/console mautic:broadcasts:send [--id=ID] [--channel=CHANNEL]

命令参数：  
*******************

- ``--channel=email`` 要执行的频道。如果未提供，默认所有频道。

- ``--id=X`` 要发送的邮件、短信或其他实体的 ID。

- ``--limit=X`` 每次从数据库拉取处理的联系人数量，默认为 100。使用此标志，每次 cron 触发时，它会处理 X 个联系人。下次 cron 作业运行时，它会处理接下来的 X 个联系人，依此类推。

- ``--batch=X`` 控制每个批次处理的邮件数量。这可能因每个提供商而异。例如，Mautic 与 SparkPost 有 API 连接。目前，他们的 API 每次调用可以发送 1000 封邮件。因此，对于此提供商，批次应为 1000 以实现最快的发送速度。许多 SMTP 提供商无法在单个批次中处理 1000 封邮件，因此需要设置得更低。

- ``--min-contact-id`` 和 ``--max-contact-id`` 允许通过指定联系人 ID 范围，将邮件发送分成更小的块。如果这些范围不重叠，这允许您并行运行多个广播命令。

.. vale off

发送预定报表定时任务  
===============================

.. vale on

从 Mautic 2.12.0 开始，可以使用 cron 来发送预定的报表。

.. code-block:: php

    php /path/to/mautic/bin/console mautic:reports:scheduler [--report=ID]

.. note::

    对于 1.1.3 之前的版本，需要在 cron 作业命令后附加 ``--env=prod`` 以确保命令正确执行。

.. vale off

配置 Mautic 集成定时任务  
======================================

.. vale on

要执行所有集成的同步并管理插件，请使用本节中的定时任务命令。

**从集成中获取联系人：**

.. code-block:: php

    php /path/to/mautic/bin/console mautic:integration:fetchleads

或

.. code-block:: php

    php /path/to/mautic/bin/console mautic:integration:synccontacts

**将联系人活动推送到集成：**

.. code-block:: php

    php /path/to/mautic/bin/console mautic:integration:pushactivity

或

.. code-block:: php

    php /path/to/mautic/bin/console mautic:integration:pushleadactivity

这些命令适用于所有可用的插件。为避免使用多个集成时出现性能问题，您必须在命令后添加 ``-integration`` 后缀来指定集成的名称。例如，对于 Mautic 与 HubSpot 的集成，请使用以下命令：

.. code-block:: php

    php /path/to/mautic/bin/console mautic:integration:fetchleads --integration=Hubspot
    php /path/to/mautic/bin/console mautic:integration:pushactivity --integration=Hubspot

**安装、更新、启用或禁用插件：**

.. code-block:: php

    php /path/to/mautic/bin/console mautic:plugins:reload

.. note::

    您可以将 ``mautic:plugins:reload`` 替换为 ``mautic:plugins:install`` 或 ``mautic:plugins:update``。
    它们是具有不同别名的相同命令。

排除已处理的实体  
**************************

此功能对于管理数据和确保实体不会被不必要地多次处理特别有用。``--exclude`` 选项可防止指定操作重新处理已经处理过的实体。此选项可用于 ``mautic:campaigns:trigger``、``mautic:campaigns:rebuild`` 和 ``mautic:segments:update`` 命令。

.. code-block:: php

    php /path/to/mautic/bin/console mautic:campaigns:trigger --exclude

.. note::

    这对于需要避免实体的冗余处理的场景特别有用，例如，防止营销活动或分组操作对同一联系人执行多次。

技巧与故障排除  
**********************

如果您的环境提供特定于命令行的 PHP 构建（通常称为 ``php-cli``），您可能希望使用它而不是 ``php``，因为它的输出更干净。在 BlueHost 以及其他一些 PHP 主机上，``php`` 命令可能被设置为丢弃传递给 ``console`` 的命令行参数，在这种情况下，您必须使用 ``php-cli`` 才能使定时任务工作。

为帮助排查定时任务问题，您可以通过在定时任务末尾添加类似 ``>>/path/to/somefile.log 2>&1`` 的内容，将每个定时任务的输出管道传输到特定文件，然后查看文件内容以查看输出。

如果运行定时任务时发生错误，此文件可以提供一些线索，否则文件为空或包含一些基本统计信息。文件的修改时间会告知您定时任务上次运行的时间。因此，您可以使用它来确定定时任务是否成功并按计划运行。

此外，建议在使用 cron 运行命令时启用非交互模式以及 no-ansi 模式。这样，您可以确保日志中具有正确的时间戳，并且输出更具可读性。

输出示例

.. code-block:: php

    php /path/to/mautic/bin/console mautic:segments:update --no-interaction --no-ansi
    [2016-09-08 06:13:57] 正在为分组 1 重建联系人
    [2016-09-08 06:13:57] 总共 0 个联系人需要以每批 300 个添加
    [2016-09-08 06:13:57] 总共 0 个联系人需要以每批 300 个移除
    [2016-09-08 06:13:57] 影响 0 个联系人

如果您有 SSH 访问权限，请尝试直接运行命令以检查错误。如果在 SSH 会话或 cron 输出中没有任何输出，请检查服务器日志。如果您看到类似 ``'Warning: Invalid argument supplied for foreach()' in /vendor/symfony/console/Symfony/Component/Console/Input/ArgvInput.php:287`` 的错误，则您需要使用 ``php-cli`` 而不是 ``php``，或者尝试使用 ``php -d register_argc_argv=On``。`