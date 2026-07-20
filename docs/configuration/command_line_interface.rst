.. vale off

命令行界面 (CLI) 指令
###########################

.. vale on

Mautic 可能要求您使用命令行（CLI）。以下列出可用的 CLI 指令。

.. note:: 

  您可以运行以下命令查看此列表（以及其他命令，例如与 Doctrine 和其他供应商相关的命令）：``bin/console``

  您必须在 Mautic 根目录中运行 CLI 指令。

**格式**: 指令 [选项] [参数]

选项
=====

.. vale off

.. list-table:: 
   :widths: 50 50
   :header-rows: 1

   * - 选项
     - 描述
   * - -h, \--help
     - 显示此帮助信息
   * - -q, \--quiet
     - 不输出任何信息
   * - | V, \--version
       |  \--ansi
       |  \--no-ansi
     - | 显示此应用的版本
       | 强制 ANSI 输出
       | 禁用 ANSI 输出
   * - -n, \--no-interaction
     - 不询问任何交互式问题
   * - | -s, \--shell
       |  \--process-isolation
     - | 启动 Shell。
       | 从 Shell 中以独立进程启动指令。
   * - | -e, \--env=ENV
       |  \--no-debug
     - | 环境名称。[默认值："prod"]
       |  关闭调试模式。
   * - | -v
       | -vv
       | -vvv
       |  \--verbose
     - | 增加信息的详细程度：
       | 1. 正常输出
       | 2. 更详细的输出
       | 3. 调试输出

.. vale on

Mautic 指令
=============
这些是您可能需要在 Mautic 实例中使用的指令。请在 Mautic 指令前加上 ``bin/console``。

**示例**

.. code-block:: shell

  bin/console mautic:segments:update

.. vale off

.. list-table:: 
   :widths: 25 50 25
   :header-rows: 1

   * - 指令
     - 描述
     - 别名
   * - ``mautic:assets:generate``
     - 合并并压缩每个捆绑包中的资源文件（CSS/JS），生成单一的生产文件
     - 
   * - ``mautic:broadcasts:send``
     - 处理待接收频道广播的联系人。
     - 
   * - ``mautic:campaigns:execute``
     - 执行特定的计划事件。
     - 
   * - ``mautic:campaigns:rebuild``
     - 根据联系人分组重建营销活动。
     - ``mautic:campaigns:update``
   * - ``mautic:campaigns:trigger``
     - 触发活跃营销活动的定时事件。
     - 
   * - ``mautic:campaigns:validate``
     - 验证联系人是否在决策中处于非活跃状态，并在满足条件时执行事件。
     - 
   * - ``mautic:citrix:sync``
     - 从 Citrix 产品同步注册者信息
     - 
   * - ``mautic:cache:clear``
     - 清除 Mautic 缓存。使用此指令将清除 Mautic 的 10 分钟缓存，其中包含分组计数和仪表盘小工具数据等内容。
     - 
   * - ``mautic:contacts:deduplicate``
     - 基于相同的唯一标识符合并联系人
     - 
   * - ``mautic:contacts:scheduled_export``
     - 将联系人导出为 CSV 文件并通过电子邮件发送结果。
     -
   * - ``mautic:custom-field:create-column``
     - 当配置选项 `create_custom_field_in_background` 设置为 true 时，在表中创建实际的列。
     - 
   * - ``mautic:custom-field:delete-column``
     - 当配置选项 `create_custom_field_in_background` 设置为 true 时，删除表中的实际列。
     - 
   * - ``mautic:email:fetch``
     - 获取并处理监控的电子邮件。
     - 
   * - ``messenger:consume email``
     - 处理邮件队列
     - 
   * - ``mautic:fields:analse``
     - 分析自定义字段表，并以表格或文件形式返回结果。参见 :doc:`/contacts/custom_fields`。
     - 
   * - ``mautic:import``
     - 如果 CSV 导入配置为后台运行，此指令将拾取待处理的导入任务，并将 CSV 文件中的数据导入 Mautic。
     - 
   * - ``mautic:integration:fetchleads``
     - 从集成模块获取联系人。
     - ``mautic:integration:synccontacts``
   * - ``mautic:integration:pipedrive:fetch``
     - 从 Pipedrive 拉取数据并发送至 Mautic
     - 
   * - ``mautic:integration:pipedrive:push``
     - 将数据从 Mautic 推送至 Pipedrive
     - 
   * - ``mautic:integration:pushleadactivity``
     - 将联系人活动推送至集成模块。
     - ``mautic:integration:pushactivity``
   * - ``mautic:install:data``
     - 安装数据
     - 
   * - ``mautic:iplookup:download``
     - 获取用于本地 IP 查找服务的远程数据存储。
     - 
   * - ``mautic:maintenance:cleanup``
     - 清理旧数据。
     - 
   * - ``mautic:remove:anonymous_contacts``
     - 从分组和营销活动成员资格中移除所有匿名联系人。
     - 
   * - ``mautic:messages:send``
     - 处理消息队列的发送。
     - ``mautic:campaigns:messagequeue``, ``mautic:campaigns:messages``
   * - ``doctrine:migrations:generate``
     - 生成一个空的迁移类。
     - 
   * - ``mautic:plugins:reload``
     - 安装、重载或更新插件。
     - ``mautic:plugins:install``, ``mautic:plugins:update``
   * - ``mautic:queue:process``
     - 处理队列
     - 
   * - ``mautic:reports:scheduler``
     - 处理报表导出的调度任务
     - 
   * - ``mautic:segments:update``
     - 基于新的联系人数据更新智能分组中的联系人。
     - ``mautic:segments:rebuild``
   * - ``mautic:segments:stat``
     - 输出所有分组的表格，并显示它们是否被用于营销活动、电子邮件、其他分组、表单操作和短信。有助于识别可以删除的分组以节省重建时的资源。
     -
   * - ``mautic:theme:json-config``
     - 将主题配置从 PHP 转换为 JSON
     - 
   * - ``mautic:unusedip:delete``
     - 删除未在任何其他数据库表中使用的 IP 地址
     - 
   * - ``mautic:update:apply``
     - 更新 Mautic 应用。
     - 
   * - ``mautic:update:find``
     - 获取 Mautic 的更新
     - 
   * - ``mautic:webhooks:process``
     - 处理队列中的 Webhook 负载
     - 
   * - ``social:monitor:twitter:hashtags``
     - 查看监控记录并查找主题标签。
     - 
   * - ``social:monitor:twitter:mentions``
     - 搜索提及的推文
     - 

.. vale on

Doctrine 指令
=================

.. list-table:: 
   :widths: 50 50
   :header-rows: 1

   * - 指令
     - 描述
   * - ``doctrine:fixtures:load``
     - 安装 Mautic 示例数据，覆盖现有数据。