.. vale off

Twilio
######

Mautic - Twilio 插件
======================

.. vale on

在您开始从 Mautic 实例发送短信之前，需要先连接到能够发送短信的服务。

首个且默认实现的服务是 :xref:`Twilio`。

为了正确配置短信，请按照以下步骤操作：

1. 在 :xref:`Twilio` 创建一个账户。

2. 在 Mautic 中，前往 *设置*（齿轮图标）> *插件*。

3. 打开 *Twilio* 插件并激活它。

4. 登录您的 Twilio 账户，前往 *仪表盘*。

 .. image:: images/twilio-sid-authtoken.png
    :width: 400
    :alt: Screenshot of the SID and Auth Token fields


5. 从 Twilio 账户复制 *账户发送者 ID (SID)*，并将其粘贴到 Twilio 插件配置中的 *账户发送者 ID* 字段。

6. 解锁并复制 *认证令牌*，并将其粘贴到 Twilio 插件配置中的 *认证令牌* 字段。

7. 在 Twilio 中前往 *电话号码* > 活跃号码，如果尚未购买号码，请添加一个电话号码。

8. 在 Twilio 中前往 *消息* > *服务*，创建一个新的消息服务。在第一步中，根据您使用 Mautic 发送短信的用途，从下拉菜单中选择适当的设置，然后点击右下角的"创建消息服务"。

 .. image:: images/twilio-messaging-services.png
    :width: 400
    :alt: Screenshot of the Messaging Services interface

9. 点击按钮将您的电话号码添加为此消息服务的发送者，然后勾选该框并点击右下角的"设置集成"以进入下一步。

10. 在集成设置下选择"发送 Webhook"。

11. 配置请求 URL 和备用 URL，使用 ``https://example.com/sms/twilio/callback`` 作为回调 URL，其中 ``example.com`` 是您的 Mautic 实例域名。同时将其填入"送达状态回调"字段。

 .. image:: images/twilio-webhook-callback.png
    :width: 400
    :alt: Screenshot of the Messaging Services interface

12. 点击"添加合规信息"按钮进入下一步，在此您可以注册使用 10 位长码电话号码发送应用到个人 (A2P) 消息。否则，点击右下角的按钮完成设置。点击"查看我的新消息服务"以查看刚刚创建的服务的详细信息。创建完成后，您可以在 消息 > 服务 页面查看其 SID。

 .. image:: images/twilio-messaging-service-id.png
    :width: 400
    :alt: Screenshot of the Messaging Services ID field on Twilio.

13. 复制消息服务 ID，并将其粘贴到 Mautic Twilio 插件设置中的"功能"标签

 .. image:: images/twilio-messaging-service-id-mautic.png
    :width: 400
    :alt: Screenshot of the Messaging Services ID field in Mautic.

14. 根据您的业务需求，为短信渠道配置全局频率规则。

15. 在 Mautic 的启用/认证标签中将 *已发布* 开关切换为 *是*，并保存插件配置。

.. vale off

字母数字发送者 ID
======================

.. vale on

字母数字发送者 ID 允许您使用个性化的发送者名称发送短信，在支持的国家/地区请参见 :xref:`International Support for Alphanumeric Sender ID`。

您无需使用 E.164 格式的 Twilio 电话号码作为"发件人"值，而是可以使用自定义字符串，如您自己企业的品牌名称。

.. note::

     您无法直接回复使用字母数字发送者 ID 发送的消息。

.. vale off

字母数字发送者 ID 要求
***********************************

.. vale on

字母数字发送者 ID 自动支持所有新的 :xref:`upgraded (paid) Twilio accounts`。不支持免费试用账户。

您可以按照以下步骤验证您的账户是否已启用字母数字发送者：

#. 登录您的 :xref:`Twilio` 账户。

#. 从左侧导航栏，点击 消息 > 概览。

#. 点击 设置。

#. 在常规消息设置页面中，验证"字母数字发送者 ID"设置。

 .. image:: images/twilio-alpha-numeric-number-settings.png
    :width: 400
    :alt: Screenshot of the Alphanumeric settings on Twilio.

.. vale off

向消息服务添加字母数字发送者 ID
====================================================

#. 通过 Twilio 仪表盘打开您的消息服务

#. 在 **发送者** 部分下，点击 **添加发送者 ID** 按钮

#. 从 **添加发送者 ID** 下拉菜单中，选择 **字母发送者**，然后输入您要添加到发送者池中的字母数字发送者 ID。

在 Twilio 网站上阅读有关 :xref:`Alphanumeric Sender ID` 的更多信息。