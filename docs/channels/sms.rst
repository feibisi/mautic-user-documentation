短信
#################

通过短信渠道，可以从 Mautic 的营销活动中发送短信。

.. note::
    要使用此渠道，您必须先设置短信传输，例如 :doc:`/plugins/twilio`。

.. vale off

短信类型
*********************

.. vale on

Mautic 允许您创建两种类型的短信，就像您可以创建不同类型的邮件一样。

.. vale off

模板短信
======================

.. vale on

模板短信由营销活动、表单、积分触发器等自动发送。您可以在创建后编辑模板短信，但不能手动将它们发送到联系人列表。

.. vale off

分组短信
=====================

.. vale on

分组短信可以手动发送到 Mautic 中的联系人列表（分组）。一旦发送，您就无法编辑该短信，但是您可以将其发送给新加入关联分组的联系人。

请注意，这些默认为营销短信，每个联系人只能接收一次该短信——原理与邮件列表相同。

您必须使用 ``发送已调度的广播`` 定时任务来启动分组短信的发送。有关更多信息，请参见 :doc:`定时任务文档 </configuration/cron_jobs>`。

.. vale off

创建短信
***********************

.. vale on

要创建短信，请导航至 渠道 > 短信 并点击"新建"按钮。

  .. image:: images/sms/sms-create-sms.png
    :width: 400
    :alt: Screenshot showing create new SMS button

选择您想创建模板短信还是分组短信，系统会显示相应的必填字段。

.. vale off

模板短信字段
============================

.. vale on

提供以下字段：

  .. image:: images/sms/sms-new-triggered-text-message-fields.png
    :width: 400
    :alt: Screenshot showing the fields required for a new Template Text Message

**内部名称** — 这是在 Mautic 内部引用此短信时使用的名称。例如，Mautic 会在营销活动构建器的下拉选择列表中使用它。

.. vale off

**短信内容** — 这是发送给联系人的短信的实际内容。字段下方有一个字数统计，帮助您确定发送完整文本所需的短信条数。您可以使用令牌，例如 ``{contactfield=firstname}``。要找到适当的令牌，请前往 设置 > 自定义字段，使用令牌格式 {contactfield=字段别名}。

.. vale on

**分类** — 这允许您选择一个分类来帮助您组织短信。

**语言** — 这允许您设置此短信的语言。

**已发布** — 这允许您设置短信的发布状态。未发布的短信不会被发送。

.. vale off

分组短信字段
============================

.. vale on

提供以下字段：

  .. image:: images/sms/sms-new-segment-sms.png
    :width: 400
    :alt: Screenshot showing the fields required for a new Segment Text Message

**内部名称** — 这是在 Mautic 内部引用此短信时使用的名称。例如，Mautic 会在营销活动构建器的下拉选择列表中使用它。

.. vale off

**短信内容** — 这是发送给联系人的短信的实际内容。字段下方有一个字数统计，帮助您确定发送完整文本所需的短信条数。您可以使用令牌，例如 ``{contactfield=firstname}``。要找到适当的令牌，请前往 设置 > 自定义字段，使用令牌格式 {contactfield=字段别名}。

.. vale on

**分类** — 这允许您选择一个分类来帮助您组织短信。

**语言** — 这允许您设置此短信的语言。

**已发布** — 这允许您设置短信的发布状态。未发布的短信不会被发送。

**联系人分组** — 这允许您定义应接收该短信的分组。

.. vale off

**发布时间（日期/时间）** — 这允许您定义此短信可发送给联系人的日期和时间

**取消发布时间（日期/时间）** — 这允许您定义此短信停止可发送给联系人的日期和时间。

从营销活动构建器创建短信
============================================

.. vale on

也可以从营销活动构建器内部创建短信。为此，选择"发送短信"营销活动操作，然后按"新建短信"按钮，而不是在下拉菜单中选择现有的短信。

  .. image:: images/sms/sms-send-sms-campaign.png
    :width: 400
    :alt: Screenshot showing the option to create an SMS from a Campaign

由于您计划在营销活动中使用此短信，它默认会被创建为模板短信，并相应地显示相关字段。

.. vale off

将短信作为营销消息发送
=============================================

.. vale on

Mautic 允许您创建一条消息——例如"今天红色鞋子有优惠！"——通过多个渠道，并通过联系人偏好的渠道来传递。这意味着他们只接收一次消息，并且是通过他们偏好的渠道接收。您可以在 :doc:`/channels/marketing_messages` 部分创建消息。

如果联系人的偏好渠道是短信，当营销消息包含短信时，Mautic 会通过短信渠道传递消息。

  .. image:: images/sms/sms-send-marketing-message.png
    :width: 400
    :alt: Screenshot showing the option to send a Text Message as a Marketing Message

管理退订
*********************

.. note::
    为了让 Mautic 处理短信退订和消息回复，您必须先配置 Webhook。有关更多信息，请查看 :doc:`/plugins/twilio` 文档。

联系人可以通过回复 ``STOP`` 或任何可接受的短语（``STOP``、``STOPALL``、``UNSUBSCRIBE``、``CANCEL``、``END`` 和 ``QUIT``）到您的短信来退订您的短信。一旦 Mautic 收到此短信，Mautic 会将特定联系人标记为短信渠道的"不联系"（DNC），并且不会再通过此渠道发送消息，除非该联系人稍后手动重新订阅。

您还可以在联系人时间线中查看短信回复：

  .. image:: images/sms/sms-contact-reply.png
    :width: 400
    :alt: Screenshot showing the reply from SMS

.. vale off

处理短信回复
*************************************

.. vale on

在 Mautic 营销活动中，当 Mautic 有活跃的短信提供商时，有一个名为"发送短信"的营销活动操作，允许您监控传入的回复以查找特定模式并据此采取行动。

  .. image:: images/sms/sms-reply-campaigns.png
    :width: 400
    :alt: Screenshot showing the Campaign action 'Sends a Text Message'

此决策跟踪对您消息的回复，并在消息中查找指定的模式。这不依赖于您先向联系人发送消息。

例如，您可以在"回复应匹配的模式"中指定"red"。如果您的消息包含语言，例如联系人使用"红色"一词回复关于他们最喜欢的鞋子颜色的问题，Mautic 会查找带有该模式的传入短信。在此示例中，您可以在决策的"是"路径上添加一个操作，将颜色偏好添加到联系人的资料中。

重要注意事项
***************

- 联系人电话号码应采用 +XXXXXXX 格式，包括 + 号且不含空格
- 联系人的手机号码字段中必须有一个电话号码
- 配置 Twilio 插件时，发送方号码必须采用 +XXXXXXX 格式，并且此号码必须与 Twilio 账户关联