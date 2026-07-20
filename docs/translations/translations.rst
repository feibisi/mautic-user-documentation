.. vale off

翻译
###########

.. vale on

作为一个拥有全球社区的国际项目，Mautic 存在许多翻译版本。如果您尚未找到您的语言，请查看有关如何 :ref:`翻译 Mautic` 的部分。

如何在 Mautic 中选择语言
**********************************

有两个地方可以选择用户界面的语言。

默认语言
================

默认语言配置首先在 Mautic 配置中进行。默认语言是 ``English - United States``。如果用户在其个人资料中未设置不同的语言，则每个用户都使用此语言。

1. 通过点击右上角的齿轮图标打开配置菜单。
2. 选择 **配置** 菜单项。
3. 选择默认语言。
4. 保存配置。

.. image:: images/translations-select-language.png
    :width: 600
    :alt: Select the default language

.. vale off

用户语言
=============

.. vale on

用户可以定义其首选语言并覆盖默认语言。这允许多语言团队在同一个 Mautic 实例上工作。

1. 通过点击右上角的用户名打开用户账户菜单。
2. 点击 **账户** 菜单项。
3. 选择用户语言。
4. 保存用户个人资料。

.. image:: images/translations-select-user-language.png
    :width: 600
    :alt: Select the user language

如何翻译 Mautic
***********************

可以将 Mautic 翻译成任何语言。由于 Mautic 是一个社区项目，任何社区成员都可以建议并将 Mautic 翻译成任何语言。Mautic 使用 :xref:`Transifex` 进行众包翻译。

1. 如果您还没有 :xref:`Transifex` 账户，请创建一个。
2. 查看 :xref:`transifex-language-list` 已存在的语言。
3. 如果您的语言缺失，请创建一种语言，或申请加入现有语言。

如果您对翻译过程有任何疑问，请查看官方 :xref:`transifex-documentation`。

如何更新语言
************************

Mautic 在保存 Mautic 配置时会自动下载语言更新（如果语言尚未下载）。要强制更新语言：

1. 通过 SFTP 或 SSH 打开 Mautic 文件系统。
2. 在 Mautic 根文件夹中，您应该看到一个名为 **translations** 的文件夹。打开它。
3. 在 **translations** 文件夹中，是 Mautic 中可用的语言。删除您要更新的语言的文件夹。
4. 转到 Mautic 配置，并在选择已删除语言的情况下保存。

Mautic 会重新下载该语言，并附带最新的翻译。有一个每日流程会从 Transifex 生成语言包。

如果您对翻译有任何疑问，请加入 :xref:`Mautic Community Slack`。

翻译覆盖
*********************

Mautic 允许您覆盖现有的语言翻译，而无需修改核心文件。这是个好主意，尤其是因为 Mautic 升级会移除您的修改。以下是正确更改翻译的方法：

例如，要覆盖第一个菜单项"仪表盘"并将其更改为"Banana"，请按照以下步骤操作：

.. image:: images/translations-dashboard.png
    :width: 600
    :alt: Override Dashboard menu item

搜索翻译键
==============================

搜索正确翻译键的最佳方法是在文本编辑器（如 VS Code）中，允许您在所有 Mautic 源代码文件中搜索文本，并按文件扩展名 ``*.ini`` 筛选这些文件。

GitHub 也有在仓库中搜索字符串的选项 —— 它不是一个特别好的搜索引擎，但对于此示例来说已经足够用了。

尝试在 Mautic/Mautic 仓库中搜索 'Dashboard menu'，因为菜单项有一个特殊的翻译，页面标题有另一个翻译。当您只搜索 'Dashboard' 时，GitHub 找不到正确的翻译 —— 它需要完整的字符串。接下来，使用筛选器仅显示 INI 文件。以下是搜索结果的链接：

:xref:`Mautic INI files`

找到的第一个文件是 ``app/bundles/DashboardBundle/Translations/en_US/messages.ini``，文件中有这一行 ``mautic.dashboard.menu.index="Dashboard"``，这就是要覆盖的文本。

.. vale off

覆盖翻译
========================

.. vale on

要覆盖的字符串是 ``mautic.dashboard.menu.index``。

要创建覆盖：

1. 转到 Mautic 项目根目录中的 ``translations`` 文件夹
2. 在其中创建一个名为 ``overrides`` 的新文件夹
3. 在此文件夹中，为要覆盖的语言区域创建文件夹。在此示例中，使用的是默认语言区域 —— ``en_US`` —— 但如果您使用其他语言，则会在 ``translations`` 文件夹中看到其语言区域作为文件夹 —— 在 overrides 文件夹中使用该语言区域的精确名称创建一个文件夹。
4. 在 ``translations/overrides/en_US`` 文件夹中 —— 将 en_US 替换为您要覆盖的语言区域 —— 创建一个名为 ``messages.ini`` 的新文件。请注意，它与原始文件名相同。必须完全一致。某些翻译可能在 ``flashes.ini`` 或 ``validators.ini`` 中，如果您覆盖这些文件中的翻译，则也必须创建正确的文件，并将要覆盖的翻译字符串添加到文件中。

在此文件中，从原始 ``app/bundles/DashboardBundle/Translations/en_US/messages.ini`` 文件中复制要覆盖的行，并按如下方式更改翻译：

``mautic.dashboard.menu.index="Banana"``

保存文件并使用 ``bin/console cache:clear`` 命令清除缓存。刷新您的 Mautic 实例，管理界面终于完美了：

.. image:: images/translations-banana.png
    :width: 600
    :alt: Dashboard menu item overridden to Banana
