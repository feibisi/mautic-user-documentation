营销消息
##################

什么是营销消息？
****************************

营销消息位于 Mautic 的渠道板块下，是您可以用来优化和个性化与客户沟通的渠道之一。

营销消息让您能够赋予客户决定权，让他们通过设置偏好的渠道来选择接收您发送内容的方式。

  .. image:: images/marketing_messages/marketing-messages.png
    :width: 200
    :alt: Screenshot showing the Marketing Messages option in the main navigation menu of Mautic.

通过营销消息，您可以创建内容并通过多个渠道提供——邮件、短信、浏览器通知、移动通知、推文，以及您使用 Mautic 可扩展开放架构决定创建的任何其他渠道。

在营销活动中使用"发送营销消息"操作时，您可以在任意或所有这些渠道中创建消息。如果联系人在其资料中设置了渠道偏好，Mautic 会通过偏好的渠道发送内容。如果联系人未指定渠道，Mautic 会使用默认渠道——邮件。

联系人还可以指定自己的频率规则，并完全暂停某个渠道的通信。当超出定义的限制并调度营销消息时，Mautic 会使用另一个有可用频率的渠道。

.. vale off

创建营销消息
****************************

.. vale on

要创建新的营销消息，请导航至渠道板块并点击营销消息。点击新建。

提供营销消息的名称和描述，然后选择您想使用的渠道。

.. note::
    您必须先设置和配置渠道，它们才会变为可用——如果您尚未设置移动通知或短信，则在创建营销消息时不会看到它们作为选项。

  .. image:: images/marketing_messages/create-marketing-message.png
    :width: 400
    :alt: Screenshot showing the creation of a new Marketing Message in Mautic.

要启用某个渠道，请将滑块点击为"是"，然后选择或创建消息。