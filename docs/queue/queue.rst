.. vale off

队列
#####

.. vale on

您可以通过激活邮件和页面打开的队列机制来提高可扩展性。如果您在人们打开页面或邮件时遇到突发的大量流量，请使用此功能。

.. note::

    使用 RabbitMQ 或 Beanstalkd 的 Mautic 3.x 用户需要直接在其本地配置文件中配置设置。如果您使用的是旧版 Mautic 2.x 系列，以下步骤保持不变。

激活
**********

您可以通过进入配置来激活和配置队列机制：

* 点击右上角的齿轮图标打开管理员菜单。
* 选择 *配置* 菜单项。
* 选择 *队列设置* 选项卡。
* 将 *队列协议* 切换为 *RabbitMQ* 或 *Beanstalkd*。
* 保存配置。

.. vale off

使用 RabbitMQ
**************

.. vale on

:xref:`RabbitMQ` 是 Mautic 支持的可用队列协议之一。要使用它，您必须有一台正在运行的 RabbitMQ 服务器。在 :xref:`RabbitMQ` 上，您可以获取有关如何安装 RabbitMQ 的说明。出于测试目的，您可以使用 :xref:`cloudamqp`，它提供 RabbitMQ 即服务。

设置好 RabbitMQ 服务器后，您可以通过在安装目录的配置文件中设置相应的 ``mautic.rabbitmq_*`` 参数来配置 Mautic 使用它。

.. list-table:: RabbitMQ
   :header-rows: 1
   :widths: 40, 40, 60

   * - 参数
     - 默认值
     - 描述
   * - ``rabbitmq_host``
     - ``'localhost'``
     - RabbitMQ 服务器的 ``hostname``
   * - ``rabbitmq_port``
     - ``'5672'``
     - RabbitMQ 服务器监听的端口
   * - ``rabbitmq_vhost``
     - ``'/'``
     - 用于此 RabbitMQ 服务器的虚拟主机
   * - ``rabbitmq_user``
     - ``'guest'``
     - RabbitMQ 服务器的用户名
   * - ``rabbitmq_password``
     - ``'guest'``
     - RabbitMQ 服务器的密码
   * - ``rabbitmq_idle_timeout``
     - ``0``
     - 	队列消费者在空闲时超时的秒数
   * - ``rabbitmq_idle_timeout_exit_code``
     - ``0``
     - 	消费者因空闲超时退出时返回的退出代码

示例：

.. code-block::

    'queue_protocol' => 'rabbitmq',
    'rabbitmq_host' => 'b-180b97c2-6b05-4b10-80ed-09182eac3a02.mq.us-west-1.amazonaws.com',
    'rabbitmq_port' => '5671',
    'rabbitmq_vhost' => '/',
    'rabbitmq_user' => 'some_user',
    'rabbitmq_password' => 'some_password',
    'rabbitmq_idle_timeout' => 0,
    'rabbitmq_idle_timeout_exit_code' => 0,


使用 Beanstalkd
****************

:xref:`Beanstalkd` 是 Mautic 支持的另一个可用队列协议。要使用它，您必须有一台正在运行的 Beanstalkd 服务器。在 :xref:`Beanstalkd website` 上，您可以获取有关如何安装 Beanstalkd 的说明。

设置好 Beanstalkd 服务器后，您可以通过在安装目录的配置文件中设置相应的 ``mautic.beanstalkd_*`` 参数来配置 Mautic 使用它。

.. list-table:: RabbitMQ
   :header-rows: 1
   :widths: 40, 40, 60

   * - 参数
     - 默认值
     - 描述
   * - ``beanstalkd_host``
     - ``'localhost'``
     - Beanstalkd 服务器的 ``hostname``
   * - ``beanstalkd_port``
     - ``'11300'``
     - Beanstalkd 服务器监听的端口
   * - ``beanstalkd_timeout``
     - ``'60'``
     - Beanstalkd 任务的默认运行时间（TTR）

处理
**********

激活队列机制后，所有页面访问和邮件打开都会被加入队列，等待后续处理。您需要定期运行一些控制台命令来处理它们。

要处理页面的访问记录，请使用以下命令：

``php /path/to/mautic/bin/console mautic:queue:process --env=prod -i page_hit``

要处理邮件的访问记录，请使用以下命令：

``php /path/to/mautic/bin/console mautic:queue:process --env=prod -i email_hit``

这些命令运行后会持续执行，直到您使用键盘组合键 ``Control + C`` 停止程序。如果您只想运行它们处理例如 50 条页面访问或邮件访问记录，可以像这样运行命令：

``php /path/to/mautic/bin/console mautic:queue:process --env=prod -i page_hit -m 50``

或

``php /path/to/mautic/bin/console mautic:queue:process --env=prod -i email_hit -m 50``

推送任务的定时任务
*********************

您需要运行以下定时任务来持续推送任务：

``php /path/to/mautic/bin/console mautic:email:send``

有关更多信息，请参阅 :ref:`定时任务<process email queue cron job>` 文档。
