移动推送通知
###########################

移动通知将您的 iOS 和 Android 应用与 :xref:`OneSignal` 集成。使用您自己的 OneSignal 账户，您现在可以在获得联系人许可的情况下向其移动设备推送通知。在 Mautic 的插件管理器中启用插件，即可在菜单的渠道下看到移动通知。

有关更多详细信息，请参阅 :xref:`OneSignal iOS` 和 :xref:`OneSignal Android` 文档。

设置
*****

.. vale off

用于 OneSignal 集成的 iOS 代码
==================================

要在您的 iOS 应用中启用推送通知，请在 ``AppDelegate`` 的 ``application`` 函数内添加以下代码（或其变体）。以下代码示例使用 Swift 3.1。如果您使用 C#，请根据需要进行修改。

.. code-block:: javascript

    // Somehow determine the user email. If you have user accounts, it may be better to move
    // this outside of the `application` func of `AppDelegate` in order to determine the user email.
    // In this example, the address is hardcoded for ease of use.
    let userEmail = "you@domain.com"

    OneSignal.initWithLaunchOptions(launchOptions, appId: "YOUR-ONE-SIGNAL-APP-ID")
    OneSignal.syncHashedEmail(userEmail);

    OneSignal.idsAvailable({(_ userId, _ pushToken) in
        let pushId      = userId != nil ? userId : ""
        let pushEnabled = pushToken != nil ? true : false
        let userData    = UserData(email: userEmail, push_id: pushId!, enabled: pushEnabled)

        self.pushUserDataToMautic(userData, "https://mautic.example.com/notification/appcallback")
    });

为便于使用，我们创建了以下结构体和函数，用于将用户数据发送到 Mautic。在您的应用中创建此结构体，并在适当的位置导入。

UserData 结构体
~~~~~~~~~~~~~~~

.. code-block:: javascript

    struct UserData {
        var email   = String()
        var push_id = String()
        var enabled = Bool()

        static func toJSON(_ userData: UserData) -> String {
            let email   = userData.email
            let pushId  = userData.push_id
            let enabled = userData.enabled

            return "{\"email\":\"\(email)\",\"push_id\":\"\(pushId)\",\"enabled\":\(enabled)}"
        }
    }

pushUserDataToMautic 函数
~~~~~~~~~~~~~~~~~~~~~~~~~

这是一个基本函数，用于将 UserData 结构体推送到您的 Mautic 安装。它会推送用户数据，然后将 Mautic 的响应作为应用弹窗显示。请根据您的应用需求进行修改。

.. code-block:: javascript

    func pushUserDataToMautic(_ userData: UserData, _ url: String) {
        var request = URLRequest(url: URL(string: url)!)
        request.httpMethod = "POST"

        let postString = UserData.toJSON(userData)
        request.httpBody = postString.data(using: .utf8)

        let task = URLSession.shared.dataTask(with: request) { data, response, error in
            guard let data = data, error == nil else {
                // check for fundamental networking error
                return
            }

            if let httpStatus = response as? HTTPURLResponse, httpStatus.statusCode != 200 {
                // check for http errors
                return
            }

            // Comment the next 4 lines to remove the alert
            let responseString = String(data: data, encoding: .utf8)
            let alert = UIAlertController(title: "Response Data", message: responseString, preferredStyle: UIAlertControllerStyle.alert)
            alert.addAction(UIAlertAction(title: "OK", style: UIAlertActionStyle.default, handler: nil))
            self.window?.rootViewController?.present(alert, animated: true, completion: nil);
        }
        task.resume()
    }

.. vale on

通知统计
=======================

除了推送到 Mautic 的 UserData 之外，您还可以通过发送 UserData 结构体并附加一个 stat JSON 键，将打开/交互统计数据推送到 Mautic。