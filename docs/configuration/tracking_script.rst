.. vale off

跟踪脚本
###############

.. vale on

在完成 :doc:`/configuration/cron_jobs` 的安装和设置后，即可开始跟踪联系人。您需要在每个希望通过 Mautic 跟踪的网站的网页中添加一段 JavaScript 代码。

这是一个简单的过程，您可以将此跟踪脚本添加到网站模板文件中，或者为更常见的内容管理系统平台安装 Mautic 集成组件。

以下是一个跟踪 JavaScript 的示例，您可以通过点击全局配置中的 **跟踪设置** 来访问该脚本。

.. code-block:: javascript

  (function(w,d,t,u,n,a,m){w['MauticTrackingObject']=n;
     w[n]=w[n]||function(){(w[n].q=w[n].q||[]).push(arguments)},a=d.createElement(t),
     m=d.getElementsByTagName(t)[0];a.async=1;a.src=u;m.parentNode.insertBefore(a,m)
    })(window,document,'script','https://example.com/mautic/mtc.js','mt');
   mt('send', 'pageview');

您应该将示例中的网站 URL ``example.com/mautic`` 替换为您的 Mautic 实例 URL，但建议直接从 Mautic 实例的跟踪设置中复制整个代码块。