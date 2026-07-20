网页通知
#################

网页通知对营销人员来说可以是一个非常强大的工具。Mautic 集成了 :xref:`OneSignal`，允许您在联系人浏览网页资源时——包括 Mautic 落地页或您自己的网站——向他们推送信息，为您提供了又一个可以用来建立关系的渠道。

Mautic 中的网页通知默认使用 OneSignal。使用您自己的 OneSignal 账户，您现在可以在获得联系人许可的情况下向其浏览器推送通知。在 Mautic 的配置中启用 OneSignal 插件，即可在菜单的渠道下看到网页通知。

有关更多信息，请参阅 OneSignal :xref:`OneSignal web push` 文档。

设置网页通知
***********************

配置
=============

#. 创建一个 OneSignal 账户，登录后创建一个应用

#. 在您的 OneSignal 应用中设置应用网站推送平台

  .. image:: images/web_notifications/onesignal_add_app.png
    :width: 400
    :alt: Screenshot showing creating push platforms on OneSignal.

#. 选择"典型站点"并填写必填字段。

.. vale off

#. 从下一个屏幕下载 SDK 文件，并将它们上传到您的 Mautic 安装根目录——必须可以通过 `https://mautic.example.com/OneSignalSDKWorker.js` 访问。

.. vale on

#. 从 OneSignal 的"设置 > 密钥和 ID"选项卡获取密钥。
#. 启用您想使用的功能——例如，是否在移动应用、落地页、您网站上被跟踪的资源上启用通知，以及是否在联系人订阅后显示欢迎通知。您还可以指定子域名，如果您使用 iOS 和 Android 通知，也可以启用这些选项——参见 :doc:`/channels/push_notifications`。

发送通知
=====================
有两种方式向联系人发送网站通知：

1. 通过营销活动操作发送
2. 通过 :doc:`/channels/marketing_messages` 发送