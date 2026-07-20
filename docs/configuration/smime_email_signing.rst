S/MIME 电子邮件签名
####################

S/MIME - 安全/多用途互联网邮件扩展 - 是一种用于对多用途互联网邮件扩展（MIME）数据进行公钥加密和签名的标准。Mautic 支持 S/MIME 电子邮件签名，以帮助验证电子邮件的真实性，并确保电子邮件内容在传输过程中未被修改。

.. note::
    目前，S/MIME 签名仅在使用 SMTP 电子邮件传输时可用。它不适用于基于 API 的电子邮件传输。

.. vale off

什么是 S/MIME 电子邮件签名？
****************************

.. vale on

S/MIME 电子邮件签名可为您的电子邮件添加数字签名，使收件人能够：

1. **验证发件人身份** - 确认电子邮件确实来自您的组织
2. **确保电子邮件完整性** - 验证电子邮件内容在传输过程中未被篡改
3. **建立信任** - 向收件人展示您的组织遵循电子邮件安全最佳实践

.. note::
    此实现仅专注于对电子邮件进行**签名**。它不加密电子邮件正文，这意味着任何有权访问的人仍可阅读电子邮件内容。许多电子邮件客户端不支持 S/MIME 加密，因此签名可以在不产生兼容性问题的情况下提供验证。

有关 S/MIME 及其使用原因的更多详细信息，请阅读 mailbox 的这篇 :xref:`S/MIME: secure Email encryption and signature` 文章。

工作原理
************

当您开启并正确配置 S/MIME 签名时：

1. Mautic 使用与发件人电子邮件地址对应的私钥签署每一封外发电子邮件
2. Mautic 将签名作为 ``smime.p7s`` 文件附加到电子邮件中
3. 使用支持 S/MIME 的电子邮件客户端的收件人可以使用公钥证书验证签名
4. 如果发件人的电子邮件地址没有对应的证书，Mautic 会在不报错的情况下发送未签名的电子邮件

开启 S/MIME 签名
**********************

通过 Mautic 配置文件开启 S/MIME 签名。该功能在 Web 界面中不可用。

.. warning::
    在开启 S/MIME 签名之前，请确保您使用的是 SMTP 电子邮件传输。此功能不适用于基于 API 的电子邮件传输。

配置
=============

将以下配置参数添加到您的 ``app/config/local.php`` 文件中：

.. code-block:: php

    <?php
    $parameters = array(
        // ... 其他配置 ...
        'smime_signing_enabled' => true,
        'smime_certificates_path' => '%kernel.project_dir%/var/smime_certificates',
    );

配置参数
------------------------

``smime_signing_enabled``
    设置为 ``true`` 可开启 S/MIME 电子邮件签名，设置为 ``false`` 则关闭。
    
    默认值：``false``

``smime_certificates_path``
    Mautic 存储 S/MIME 证书的目录的绝对路径。您可以使用 ``%kernel.project_dir%`` 来引用您的 Mautic 安装目录。
    
    默认值：``%kernel.project_dir%/var/smime_certificates``

生成 S/MIME 证书
******************************

从 Mautic 发送电子邮件的每个电子邮件地址都需要自己的证书对：

- 一个**公钥证书** - ``.crt`` 文件 - 用于验证您的身份
- 一个**私钥** - ``.pem`` 文件 - 用于签署电子邮件

自签名证书
========================

出于测试目的，您可以创建自签名证书。但是，对于生产环境，您应从受信任的证书颁发机构获取证书。

要创建自签名证书和私钥：

.. code-block:: bash

    # 创建私钥和证书签名请求
    openssl req -newkey rsa:4096 -nodes -keyout sender@example.com.pem -out sender@example.com.csr
    
    # 创建有效期为 1 年的自签名证书
    openssl x509 -req -days 365 -in sender@example.com.csr -signkey sender@example.com.pem -out sender@example.com.crt

.. important::
    将 ``sender@example.com`` 替换为您用于从 Mautic 发送电子邮件的实际电子邮件地址。

生产环境证书
=======================

对于生产环境，请从受信任的证书颁发机构（CA）获取 S/MIME 证书。许多证书颁发机构提供 S/MIME 证书，该过程通常包括：

1. 生成证书签名请求 (CSR)
2. 将 CSR 连同身份验证文件一起提交给 CA
3. 从 CA 接收签名的证书

要查看此过程在实际中如何运作的示例，请参阅 Mozilla 的这篇 :xref:`Mozilla guide on obtaining S/MIME certificates` 文章。

安装证书
***********************

证书文件命名
=======================

根据证书对应的电子邮件地址命名证书：

- 公钥证书：``email@example.com.crt``
- 私钥：``email@example.com.pem`` - 纯文本 - 或 ``email@example.com.pem.enc`` - 加密

将 ``email@example.com`` 替换为实际的发件人电子邮件地址。

.. important::
    文件名中的电子邮件地址必须与发送电子邮件时使用的**发件人**地址完全匹配。

证书目录结构
===============================

将您的证书文件放置在 ``smime_certificates_path`` 指定的目录中：

.. code-block:: text

    /var/smime_certificates/
    ├── admin@example.com.crt
    ├── admin@example.com.pem
    ├── support@example.com.crt
    └── support@example.com.pem

设置权限
===================

确保 Web 服务器用户对证书目录和文件具有读取权限：

.. code-block:: bash

    # 设置所有者（将 www-data 替换为您的 Web 服务器用户）
    chown -R www-data:www-data /path/to/mautic/var/smime_certificates
    
    # 设置目录权限
    chmod 755 /path/to/mautic/var/smime_certificates
    
    # 设置证书权限
    chmod 644 /path/to/mautic/var/smime_certificates/*.crt
    chmod 600 /path/to/mautic/var/smime_certificates/*.pem

.. warning::
    私钥（``.pem`` 文件）应具有限制性权限（``600``），以防止未经授权的访问。

加密私钥
***********************

为了增强安全性，您可以使用 Mautic 的加密系统加密您的私钥。Mautic 将加密的私钥以 ``.pem.enc`` 扩展名存储。

加密的好处
======================

加密私钥增加了额外的安全层：

- 如果有人入侵了您的服务器，没有 Mautic 的密钥，他们就无法使用加密的密钥
- 加密使用 Mautic 实例配置中的 ``secret_key``
- Mautic 在需要签署电子邮件时自动解密密钥

.. important::
    确保您在 ``app/config/local.php`` 文件中配置了 ``secret_key``。Mautic 在安装过程中会自动创建它。

创建加密密钥
=======================

要加密现有的私钥：

1. 确保您的 ``secret_key`` 已在 ``app/config/local.php`` 中配置
2. 使用 Mautic 的加密辅助工具或命令行：

.. code-block:: bash

    # 使用 PHP 加密密钥
    php -r "
    require 'app/config/local.php';
    require 'app/bundles/CoreBundle/Helper/EncryptionHelper.php';
    \$helper = new \Mautic\CoreBundle\Helper\EncryptionHelper(
        new \Mautic\CoreBundle\Helper\CoreParametersHelper(new \Symfony\Component\DependencyInjection\ParameterBag\ParameterBag(\$parameters))
    );
    \$key = file_get_contents('var/smime_certificates/sender@example.com.pem');
    file_put_contents('var/smime_certificates/sender@example.com.pem.enc', \$helper->encrypt(\$key));
    "

3. 创建加密版本后，为了安全起见，您可以删除纯文本的 ``.pem`` 文件
4. 如果存在，Mautic 会自动使用加密版本（``.pem.enc``）

密钥优先级
============

当查找私钥时，Mautic 按以下顺序检查：

1. 加密密钥：``email@example.com.pem.enc``
2. 纯文本密钥：``email@example.com.pem``

如果两者都存在，则加密版本优先。

测试 S/MIME 签名
**********************

配置 S/MIME 签名后：

1. 使用已配置证书的电子邮件地址从 Mautic 发送一封测试邮件
2. 在您的电子邮件客户端中查看电子邮件的来源/标头
3. 查找以下表明 Mautic 已签署电子邮件的迹象：

   - Content-Type 标头包含 ``multipart/signed``
   - 有一个名为 ``smime.p7s`` 的附件
   - protocol ``application/x-pkcs7-signature``

4. 如果您的电子邮件客户端支持 S/MIME，您应该会看到一个验证指示符，例如印章或复选标记

S/MIME 故障排除
**********************

电子邮件未被签名
====================

如果 Mautic 未签署电子邮件，请检查：

1. **S/MIME 已启用** - 验证 ``smime_signing_enabled`` 在 ``local.php`` 中设置为 ``true``
2. **使用 SMTP 传输** - S/MIME 仅适用于 SMTP。检查您的电子邮件传输设置
3. **证书存在** - 确认 ``.crt`` 和 ``.pem`` 文件存在于证书目录中
4. **文件名正确** - 证书文件名必须与发件人电子邮件地址完全匹配
5. **文件权限** - Web 服务器用户必须对证书文件具有读取权限
6. **检查日志** - 在 ``var/logs/mautic_prod.log`` 中查找任何与 S/MIME 相关的错误

未找到证书错误
=============================

如果您在日志中看到证书错误：

1. 验证 ``smime_certificates_path`` 在您的配置中是否正确指定
2. 确保 Mautic 正确命名了证书文件（``email@example.com.crt`` 和 ``.pem``）
3. 确保文件名中的电子邮件地址与发件人地址完全匹配
4. 验证文件权限是否允许 Web 服务器用户读取文件

证书验证错误
=============================

如果收件人报告证书验证错误：

1. **自签名证书** - 默认情况下不受信任。收件人需要手动信任它们
2. **证书已过期** - 检查您的证书有效日期
3. **证书链** - 确保您使用的是来自证书颁发机构的完整证书链
4. **域名不匹配** - 证书中的电子邮件地址必须与发件人地址匹配

性能考量
==========================

S/MIME 签名会为每封电子邮件增加少量处理开销：

- Mautic 为每封电子邮件单独执行签名
- 开启 S/MIME 后，Mautic 会关闭批量电子邮件处理（基于令牌的发送）以确保正确签名
- 对于高容量电子邮件发送，请监控您的服务器资源

限制
***********

Mautic 中 S/MIME 签名的当前限制：

1. **仅限 SMTP** - S/MIME 签名仅适用于 SMTP 电子邮件传输。不支持基于 API 的传输。
2. **仅签名** - 此实现签署电子邮件，但不加密电子邮件正文。内容仍然可读。
3. **无批处理** - 开启 S/MIME 后，Mautic 会关闭批量电子邮件处理（基于令牌的发送）以确保正确签名。
4. **每次请求一封邮件** - Mautic 单独发送每封电子邮件，而不是分批发送。

.. note::
    如果您开启了 S/MIME 签名但使用的是非 SMTP 传输，Mautic 会强制每次请求只发送一封电子邮件，但签名可能无法正常工作。始终使用 SMTP 进行 S/MIME 签名。

其他资源
*********************

有关 S/MIME 的更多信息：

- :xref:`S/MIME: secure Email encryption and signature`
- :xref:`Mozilla guide on obtaining S/MIME certificates`
- :xref:`OpenSSL Documentation`

相关文档
*********************

.. vale off

- :doc:`/configuration/settings` - 通用电子邮件设置配置
- :doc:`/channels/emails` - 电子邮件概述与管理
- :doc:`/configuration/cron_jobs` - 设置用于电子邮件发送的 Cron 任务

.. vale on