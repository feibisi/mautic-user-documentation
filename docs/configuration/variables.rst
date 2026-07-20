变量
#########

.. tip:: 
  默认值

  默认值 - 有时称为回退文本 - 在 ``|`` 字符后指定。例如，请考虑以下邮件问候语：

  ``Hi {contactfield=firstname|there},``

令牌修饰符
***************

选择型和布尔型字段的标签修饰符
============================================

对于选择型和布尔型字段，您可以使用 ``|label`` 修饰符来显示人类可读的标签，而不是存储的值。当您的选择字段存储代码或 ID 等值，但您希望向联系人显示友好的标签时，这将非常有益。

**语法：**

.. code-block:: text

   {contactfield=field_alias|label}

**示例：**

* 对于别名为 ``country_select`` 的选择字段，若其选项如 ``us`` 对应 ``United States`` 或 ``uk`` 对应 ``United Kingdom``：

   * ``{contactfield=country_select}`` 显示值 ``us``
   * ``{contactfield=country_select|label}`` 显示标签 ``United States``

* 对于别名为 ``is_subscriber`` 的布尔型字段：

   * ``{contactfield=is_subscriber}`` 显示值 ``1`` 或 ``0``
   * ``{contactfield=is_subscriber|label}`` 显示标签 ``Yes`` 或 ``No``

* 同时适用于联系人字段和公司字段：

   * ``{contactfield=company_type|label}`` 显示公司选择字段的标签
   * ``{contactfield=company_active|label}`` 显示公司布尔型字段的标签

.. note::

   ``|label`` 修饰符仅适用于选择型和布尔型字段。对于其他字段类型，它将显示常规值。

联系人字段
**************

更多信息请参见 :doc:`管理自定义字段 </contacts/custom_fields>`。

.. list-table:: 
   :widths: 100 100
   :header-rows: 1

   * - 变量名称
     - 变量语法
   * - 归因
     - ``{contactfield=attribution}``
   * - 归因日期
     - ``{contactfield=attribution_date}``
   * - 地址行 1
     - ``{contactfield=address1}``
   * - 地址行 2
     - ``{contactfield=address2}``
   * - 国家/地区
     - ``{contactfield=country}``
   * - 城市
     - ``{contactfield=city}``
   * - 公司
     - ``{contactfield=company}``
   * - 联系人 ID
     - ``{contactfield=id}``
   * - 邮箱
     - ``{contactfield=email}``
   * - Facebook
     - ``{contactfield=facebook}``
   * - 传真
     - ``{contactfield=fax}``
   * - 名字
     - ``{contactfield=firstname}``
   * - Foursquare
     - ``{contactfield=foursquare}``
   * - Google+
     - ``{contactfield=googleplus}``
   * - Instagram
     - ``{contactfield=instagram}``
   * - IP 地址
     - ``{contactfield=ipAddress}``
   * - 姓氏
     - ``{contactfield=lastname}``
   * - LinkedIn
     - ``{contactfield=linkedin}``
   * - 手机号码
     - ``{contactfield=mobile}``
   * - 电话号码
     - ``{contactfield=phone}``
   * - 职位
     - ``{contactfield=position}``
   * - Skype
     - ``{contactfield=skype}``
   * - 州/省
     - ``{contactfield=state}``
   * - Twitter
     - ``{contactfield=twitter}``
   * - 称呼
     - ``{contactfield=title}``
   * - 网站
     - ``{contactfield=website}``
   * - 邮政编码
     - ``{contactfield=zipcode}``
  
联系人所有者字段
*********************
  
.. list-table:: 
   :widths: 100 100
   :header-rows: 1
  

   * - 变量名称
     - 变量语法
   * - 名字
     - ``{ownerfield=firstname}``
   * - 姓氏
     - ``{ownerfield=lastname}``
   * - 邮箱
     - ``{ownerfield=email}``
   * - 职位
     - ``{ownerfield=position}``
   * - 签名
     - ``{ownerfield=signature}``

公司联系人字段
***********************

更多信息请参见 :doc:`公司</companies/companies_overview>`。

.. list-table:: 
   :widths: 100 100
   :header-rows: 1

   * - 变量名称
     - 变量语法
   * - 地址行 1（公司）
     - ``{contactfield=companyaddress1}``
   * - 地址行 2（公司）
     - ``{contactfield=companyaddress2}``
   * - 年收入（公司）
     - ``{contactfield=companyannual_revenue}``
   * - 城市（公司）
     - ``{contactfield=companycity}``
   * - 国家/地区（公司）
     - ``{contactfield=companycountry}``
   * - 描述（公司）
     - ``{contactfield=companydescription}``
   * - 邮箱（公司）
     - ``{contactfield=companyemail}``
   * - 传真（公司）
     - ``{contactfield=companyfax}``
   * - 行业（公司）
     - ``{contactfield=companyindustry}``
   * - 名称
     - ``{contactfield=companyname}``
   * - 员工数（公司）
     - ``{contactfield=companynumber_of_employees}``
   * - 电话号码（公司）
     - ``{contactfield=companyphone}``
   * - 州/省（公司）	
     - ``{contactfield=companystate}``
   * - 网站（公司）
     - ``{contactfield=companywebsite}``
   * - 邮政编码（公司）
     - ``{contactfield=companyzipcode}``

.. tip::
  
   **自定义公司字段**

   自定义公司字段的语法与核心公司字段语法不同。您**不得**在变量中添加“公司”字样，而应将其视为 ``contactfield``。

Mautic 组件令牌
***********************

更多信息请参见 :doc:`组件</components/assets>` 和 :doc:`管理页面</components/landing_pages>`。

.. list-table:: 
   :widths: 100 100
   :header-rows: 1
  

   * - 变量名称
     - 变量语法
   * - 资源 ID# 的资源链接
     - ``{assetlink=25}``
   * - 焦点项目 ID#
     - ``{focus=4}``
   * - 表单 ID#
     - ``{form=83}``
   * - 页面 ID# 的着陆页链接
     - ``{pagelink=17}``

邮件专用令牌
*********************

更多信息请参见 :doc:`管理邮件</channels/emails>`。

.. list-table:: 
   :widths: 100 100
   :header-rows: 1
  

   * - 变量名称
     - 变量语法
   * - 签名
     - ``{signature}``
   * - 主题
     - ``{subject}``
   * - 跟踪像素
     - ``{tracking_pixel}``
   * - 取消订阅文本
     - ``{unsubscribe_text}``
   * - 取消订阅 URL
     - ``{unsubscribe_url}``
   * - 重新订阅 URL
     - ``{resubscribe_url}``
   * - 网页视图文本
     - ``{webview_text}``
   * - 网页视图 URL
     - ``{webview_url}``

着陆页令牌
*********************

更多信息请参见 :doc:`/components/landing_pages`。

.. list-table:: 
   :widths: 100 100
   :header-rows: 1
  

   * - 变量名称
     - 变量语法
   * - 元描述
     - ``{pagemetadescription}``
   * - 标题
     - ``{pagetitle}``
   * - 语言栏
     - ``{langbar}``
   * - 分享按钮
     - ``{sharebuttons}``
   * - 成功消息
     - ``{successmessage}``

偏好中心着陆页令牌
*************************************

更多信息请参见 :doc:`自定义偏好中心</contacts/preference_center>`。

.. list-table:: 
   :widths: 100 100
   :header-rows: 1
  

   * - 变量名称
     - 变量语法
   * - 线索标识符
     - ``{leadidentifier}``
   * - 分类列表
     - ``{categorylist}``
   * - 分组列表
     - ``{segmentlist}``
   * - 首选渠道
     - ``{preferredchannel}``
   * - 渠道频率
     - ``{channelfrequency}``
   * - 保存偏好
     - ``{saveprefsbutton}``

动态 Web 内容令牌
**************************

.. list-table:: 
   :widths: 100 100
   :header-rows: 1
  

   * - 变量名称
     - 变量语法
   * - [动态内容 1] | 例如用户定义的变量名
     - ``{dynamiccontent="Dynamic Content 1"}``

联系人监控
******************

更多信息请参见 :ref:`联系人监控<Contact tracking>`。

.. list-table:: 
   :widths: 100 100
   :header-rows: 1
  

   * - 变量名称
     - 变量语法
   * - 语言
     - ``{language}``
   * - 标题
     - ``{title}``
   * - 着陆页标题
     - ``{page_title}``
   * - URL
     - ``{url}``   
   * - 着陆页 URL
     - ``{page_url}``
   * - 引荐来源
     - ``{referrer}``
   * - 跟踪像素
     - ``{tracking_pixel}``
   * - UTM 营销活动
     - ``{utm_campaign}``
   * - UTM 内容
     - ``{utm_content}``
   * - UTM 媒介
     - ``{utm_medium}``
   * - UTM 来源
     - ``{utm_source}``
   * - UTM 关键词
     - ``{utm_term}``

搜索过滤器
**************

更多信息请参见 :ref:`搜索<search>` 页面。

字母顺序列表
*****************

.. list-table:: 
   :widths: 40 50
   :header-rows: 1

   * - 变量名称
     - 变量语法
   * - 地址行 1
     - ``{contactfield=address1}``
   * - 地址行 1（公司）
     - ``{contactfield=address1}``
   * - 地址行 2
     - ``{contactfield=address2}``
   * - 地址行 2（公司）
     - ``{contactfield=companyaddress2}``
   * - 年收入（公司）
     - ``{contactfield=companyannual_revenue}``
   * - 资源 ID# 的资源链接
     - ``{assetlink=25}``
   * - 归因
     - ``{contactfield=attribution}``
   * - 归因日期
     - ``{contactfield=attribution_date}``
   * - 分类列表（偏好中心）
     - ``{categorylist}``
   * - 渠道频率（偏好中心）
     - ``{channelfrequency}``
   * - 城市
     - ``{contactfield=city}``
   * - 城市（公司）
     - ``{contactfield=companycity}``
   * - 国家/地区
     - ``{contactfield=country}``
   * - 国家/地区（公司）
     - ``{contactfield=companycountry}``
   * - 公司
     - ``{contactfield=company}``
   * - 联系人 ID
     - ``{contactfield=id}``
   * - 描述（公司）
     - ``{contactfield=companydescription}``
   * - [动态内容 1]例如：用户定义的变量名
     - ``{dynamiccontent="Dynamic Content 1"}``
   * - 邮箱
     - ``{contactfield=email}``
   * - 邮箱（公司）
     - ``{contactfield=companyemail}`` 
   * - Facebook
     - ``{contactfield=facebook}``
   * - 传真
     - ``{contactfield=fax}``
   * - 焦点项目 ID#
     - ``{focus=4}``
   * - 表单 ID#
     - ``{form=83}`` 
   * - 传真（公司）
     - ``{contactfield=companyfax}`` 
   * - 名字
     - ``{contactfield=firstname}``
   * - Foursquare
     - ``{contactfield=foursquare}``
   * - Google+
     - ``{contactfield=googleplus}``
   * - Instagram
     - ``{contactfield=instagram}``
   * - IP 地址
     - ``{contactfield=ipAddress}``
   * - 页面 ID# 的着陆页链接
     - ``{pagelink=17}``
   * - 语言栏
     - ``{langbar}`` 
   * - 姓氏
     - ``{contactfield=lastname}``
   * - 联系人标识符（偏好中心）
     - ``{leadidentifier}``  
   * - LinkedIn
     - ``{contactfield=linkedin}``
   * - 元描述（着陆页）
     - ``{pagemetadescription}``  
   * - 手机号码
     - ``{contactfield=mobile}``
   * - 名称（公司）	
     - ``{contactfield=companyname}``
   * - 员工数（公司）	
     - ``{contactfield=companynumber_of_employees}`` 
   * - 电话号码
     - ``{contactfield=phone}`` 
   * - 电话号码（公司）
     - ``{contactfield=companyphone}`` 
   * - 职位
     - ``{contactfield=position}``
   * - 保存偏好（偏好中心）	
     - ``{saveprefsbutton}`` 
   * - 分组列表（偏好中心）
     - ``{segmentlist}`` 
   * - 签名
     - ``{signature}`` 
   * - Skype
     - ``{contactfield=skype}``
   * - 州/省
     - ``{contactfield=state}``
   * - 州/省（公司）
     - ``{contactfield=companystate}``
   * - 主题
     - ``{subject}`` 
   * - Twitter
     - ``{contactfield=twitter}``
   * - 首选渠道（偏好中心）
     - ``{preferredchannel}``
   * - 重新订阅 URL
     - ``{resubscribe_url}``
   * - 分享按钮
     - ``{sharebuttons}``
   * - 成功消息
     - ``{successmessage}`` 
   * - 称呼
     - ``{contactfield=title}``
   * - 标题（着陆页）
     - ``{pagetitle}`` 
   * - 取消订阅文本
     - ``{unsubscribe_text}``
   * - 取消订阅 URL
     - ``{unsubscribe_url}`` 
   * - 网站
     - ``{contactfield=website}``
   * - 网站（公司）
     - ``{contactfield=companywebsite}``
   * - 网页视图文本
     - ``{webview_text}`` 
   * - 网页视图 URL
     - ``{{webview_url}`` 
   * - 邮政编码
     - ``{contactfield=zipcode}``
   * - 邮政编码（公司）
     - ``{contactfield=companyzipcode}`` 
  