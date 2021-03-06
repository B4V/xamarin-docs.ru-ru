---
title: Ручная подготовка для Xamarin.iOS
description: После успешной установки Xamarin.iOS следующим шагом в разработке приложений для iOS является подготовка устройства iOS. Это руководство описывает, как использовать ручную подготовку для настройки сертификатов и профилей разработки.
ms.prod: xamarin
ms.assetid: E26ACC94-F4A5-4FF5-B7D4-BE596745A665
ms.technology: xamarin-ios
author: asb3993
ms.author: amburns
ms.date: 07/15/2017
ms.openlocfilehash: 3f74144f85cc045b4ea9807d3d818677e33539f2
ms.sourcegitcommit: e268fd44422d0bbc7c944a678e2cc633a0493122
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50123470"
---
# <a name="manual-provisioning-for-xamarinios"></a>Ручная подготовка для Xamarin.iOS

_Установив Xamarin.iOS для разработки приложений для iOS можно приступать к подготовке устройства iOS. Это руководство описывает, как использовать ручную подготовку для настройки сертификатов и профилей разработки._

> [!NOTE]
> Инструкции на этой странице предназначены для разработчиков с платным доступом к программе для разработчиков Apple. Если у вас бесплатная учетная запись, обратитесь к руководству [Бесплатная подготовка](~/ios/get-started/installation/device-provisioning/free-provisioning.md) для получения дополнительных сведений о тестировании на устройствах.

## <a name="creating-a-signing-identity"></a>Создание удостоверения подписывания

Первым шагом в настройке устройства для разработки является создание удостоверения подписывания. Удостоверение подписывания состоит из двух компонентов:

- сертификата разработки;
- закрытого ключа.

Сертификаты разработки и связанные [ключи](#understanding-certificate-key-pairs) критически важны для разработчика iOS: они являются его удостоверением в Apple и связывают его с определенным устройством и профилем разработки. Они действуют подобно цифровой подписи, добавляемой к приложению. Apple проверяет сертификаты для управления доступом к устройствам, на которых разрешено развертывание.

Командами разработчиков, сертификатами и профилями можно управлять в разделе [Сертификаты, идентификаторы и профили](https://developer.apple.com/account/overview.action) (требуется вход в систему) в Центре пользователей Apple. Apple требует наличия удостоверения подписывания для создания кода для устройства или симулятора.  

> [!IMPORTANT]
> Важно отметить, что одновременно можно иметь только два сертификата разработки iOS. Чтобы создать еще один сертификат, необходимо отозвать один из имеющихся. Компьютер с отозванным сертификатом не сможет подписать приложение.

Чтобы создать удостоверение подписывания, выполните указанные ниже действия:

1. Войдите в [раздел Certificates, Identifiers and Profiles (Сертификаты, идентификаторы и профили) на портале разработчика](https://developer.apple.com/account/overview.action) и выберите в столбце **iOS Apps** (Приложения iOS) раздел **Certificates** (Сертификаты). Чтобы создать сертификат, нажмите кнопку **+**:

    [![](manual-provisioning-images/cert-plus.png "Нажмите кнопку \"+\", чтобы создать сертификат")](manual-provisioning-images/cert-plus.png#lightbox)

2. В качестве типа сертификата выберите **iOS App Development** (Разработка приложений для iOS), после чего нажмите кнопку **Continue** (Продолжить). В зависимости от прав вашей учетной записи этот экран может выглядеть иначе:

    [![](manual-provisioning-images/cert-first.png "Выбор типа сертификата \"Разработка приложений для iOS\"")](manual-provisioning-images/cert-first.png#lightbox)

3. Отправьте запрос на подписание сертификата, который необходим для создания сертификата вручную. Для этого запустите на компьютере Mac программу **Keychain Access** (Доступ к связке ключей). В главном меню выберите пункт **Certificate Assistant** (Помощник по сертификатам), а затем пункт **Request a Certificate from a Certificate Authority...** (Запросить сертификат из центра сертификации...), как показано ниже:

      [![](manual-provisioning-images/key-first.png "Запрос подписи сертификата")](manual-provisioning-images/key-first.png#lightbox)

4. Введите сведения о себе и выберите вариант **Save to disk** (Сохранить на диск):

    [![](manual-provisioning-images/key-second.png "Заполнение сведений о себе")](manual-provisioning-images/key-second.png#lightbox)

5. Сохраните запрос подписи сертификата в месте, где его легко будет найти:

    [![](manual-provisioning-images/cert-third.png "Сохранение запроса подписи сертификата")](manual-provisioning-images/cert-third.png#lightbox)

6. Вернитесь на портал подготовки, добавьте на него сертификат и отправьте его:

    [![](manual-provisioning-images/cert-second.png "Добавление сертификата на портал")](manual-provisioning-images/cert-second.png#lightbox)

    Если у вас нет прав администратора, сертификат должен быть утвержден администратором или агентом рабочей группы.

7. После утверждения сертификата скачайте его с портала подготовки:

    [![](manual-provisioning-images/status-dev.png "Скачивание сертификата с портала подготовки")](manual-provisioning-images/status-dev.png#lightbox)

8. Дважды щелкните скачанный сертификат, чтобы запустить программу Keychain Access, и откройте панель **My Certificates** (Мои сертификаты), в которой показан новый сертификат и связанный закрытый ключ:

    [![](manual-provisioning-images/keychain.png "Сертификат в программе Keychain Access")](manual-provisioning-images/keychain.png#lightbox)

### <a name="understanding-certificate-key-pairs"></a>Основные сведения о парах ключей сертификатов

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio для Mac](#tab/macos)

Профиль разработчика содержит сертификаты, связанные с ними ключи, а также профили подготовки, связанные с учетной записью. По сути, существуют две версии профиля разработчика: одна на портале разработчика, а другая на локальном компьютере Mac. Различие между ними — в типе ключей, которые они содержат: _профиль на портале вмещает все открытые ключи, связанные с вашими сертификатами, а копия на локальном компьютере Mac содержит все закрытые ключи_. Чтобы сертификаты были действительны, пары ключей должны совпадать. Храните резервную копию профиля разработчика на локальном компьютере Mac, так как в случае утери закрытых ключей все сертификаты и профили подготовки потребуется создать заново.

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

Профиль разработчика содержит сертификаты, связанные с ними ключи, а также профили подготовки, связанные с учетной записью. По сути, существуют две версии профиля разработчика: одна на портале разработчика, а другая на компьютере Mac. Различие между ними — в типе ключей, которые они содержат: _профиль на портале вмещает все открытые ключи, связанные с вашими сертификатами, а копия на компьютере Mac содержит все закрытые ключи_. Чтобы сертификаты были действительны, пары ключей должны совпадать. Храните резервную копию профиля разработчика на компьютере Mac с узлом сборки Xamarin, так как в случае утери закрытых ключей все сертификаты и профили подготовки потребуется создать заново.

-----

> [!WARNING]
> Потеря сертификата и связанных с ним ключей может надолго остановить работу, так как потребуется отозвать существующие сертификаты и повторно подготовить все связанные устройства, включая зарегистрированные для специального развертывания. Успешно настроив сертификаты разработки, экспортируйте резервную копию и сохраните ее в надежном месте. Дополнительные сведения о выполнении этой задачи см. в разделе "Exporting and Importing Certificates and Profiles" (Экспорт и импорт сертификатов и профилей) руководства [Maintaining Certificates](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html) (Обслуживание сертификатов) в документации Apple.

<a name="provisioning" />

## <a name="provisioning-an-ios-device-for-development"></a>Подготовка устройства iOS к разработке

Создав удостоверение в Apple и получив сертификат разработки, необходимо настроить профиль подготовки и требуемые сущности, чтобы получить возможность развертывать приложение на устройстве Apple. На устройстве должна быть версия iOS, поддерживаемая Xcode. Может потребоваться обновить устройство, среду Xcode или и то, и другое.

<a name="adddevice" />

## <a name="add-a-device"></a>Добавление устройства

При создании профиля подготовки для разработки необходимо указать, на каких устройствах может выполняться приложение. Для этого на портал разработки можно добавить до 100 устройств за календарный год, а затем выбрать из их числа те устройства, которые следует добавить в определенный профиль подготовки. Чтобы добавить устройство на портал разработки, на компьютере Mac сделайте следующее.

1. Запустите Xcode.
2. Подключите подготавливаемое устройство к компьютеру Mac с помощью USB-кабеля из комплекта поставки.
2. В меню **Window** (Окно) выберите пункт **Devices** (Устройства):

  [![](manual-provisioning-images/add01.png "В меню \"Окно\" выберите \"Устройства\"")](manual-provisioning-images/add01.png#lightbox)

3. В списке **DEVICES** (Устройства) в левой части окна Devices выберите нужно устройство iOS.
4. Выделите строку в поле **Identifier** (Идентификатор) и скопируйте ее в буфер обмена:

  [![](manual-provisioning-images/add02.png "Выделение строки идентификатора")](manual-provisioning-images/add02.png#lightbox)

5. В браузере Safari перейдите в [Apple Developer Center](https://developer.apple.com/membercenter/index.action) и выполните вход.
6. Щелкните ссылку **Certificates, Identifiers & Profiles** (Сертификаты, идентификаторы и профили):

  [![](manual-provisioning-images/add03.png "Щелкните ссылку \"Сертификаты, идентификаторы и профили\"")](manual-provisioning-images/add03.png#lightbox)

7. Щелкните ссылку **Devices** (Устройства):

  [![](manual-provisioning-images/add04.png "Щелкните ссылку \"Устройства\"")](manual-provisioning-images/add04.png#lightbox)

8. Нажмите кнопку **+**:

  [![](manual-provisioning-images/add05.png "Нажмите кнопку \"+\"")](manual-provisioning-images/add05.png#lightbox)

9. Укажите имя нового устройства и вставьте **идентификатор** устройства, скопированный ранее, в поле **UUID**:

  [![](manual-provisioning-images/add06.png "Укажите имя нового устройства и его идентификатор")](manual-provisioning-images/add06.png#lightbox)

10. Нажмите кнопку **Continue** (Продолжить).
11. Наконец, проверьте сведения и нажмите кнопку **Register** (Зарегистрировать):

  [![](manual-provisioning-images/add07.png "Проверка сведений")](manual-provisioning-images/add07.png#lightbox)

Повторите описанные выше действия для всех устройств iOS, которые будут использоваться для тестирования или отладки приложения Xamarin.iOS.

После добавления устройства на портал разработчика необходимо создать профиль подготовки и добавить в него устройство.

<a name="provisioningprofile" />

## <a name="creating-a-development-provisioning-profile"></a>Создание профиля подготовки для разработки

Так же как и сертификат разработки, профили подготовки можно создать вручную в разделе [Certificates, Identifiers & Profiles](https://developer.apple.com/account/overview.action) (Сертификаты, идентификаторы и профили) центра Apple Members Center.

Перед созданием профиля подготовки необходимо создать *идентификатор приложения*. Идентификатор приложения — это строка в обратном стиле DNS, однозначно определяющая приложение. Ниже показано, как создать **шаблон идентификатора приложения**, который можно использовать для создания и установки большинства приложений. **Явный идентификатор приложения** позволяет устанавливать только одно приложение (с соответствующим идентификатором пакета) и, как правило, применяется для определенных функций iOS, таких как Apple Pay и HealthKit. Сведения о создании явных идентификаторов приложений см. в руководстве [Работа с возможностями](~/ios/deploy-test/provisioning/capabilities/index.md).

### <a name="app-id"></a>Идентификатор приложения

1. На [портале разработчика](https://developer.apple.com/account/overview.action) перейдите в раздел *Certificates, Identifiers and Profiles* (Сертификаты, идентификаторы и профили) в Apple Developer Center. В разделе **Identifiers** (Идентификаторы) выберите элемент **App IDs** (ИД приложений).
2. Нажмите кнопку **+** и укажите **имя**:

    [![](manual-provisioning-images/appid05a.png "Укажите имя")](manual-provisioning-images/appid05a.png#lightbox)
3. Префикс приложения должен быть предварительно задан. Выберите вариант **Wildcard App ID** (Шаблон ИД приложения) в качестве суффикса приложения. Введите идентификатор пакета в формате `com.[DomainName].*`:

  [![](manual-provisioning-images/appid05b.png "Введите идентификатор пакета")](manual-provisioning-images/appid05b.png#lightbox)

3. Нажмите кнопку **Continue** (Продолжить) и следуйте инструкциям на экране, чтобы создать идентификатор приложения.

### <a name="provisioning-profile"></a>Профиль подготовки

После создания идентификатора приложения можно создать профиль подготовки. Профиль подготовки содержит сведения о том, с *каким* приложением (или приложениями в случае с шаблоном идентификатора приложения) связан этот профиль, *кто* может его использовать (в зависимости от добавленных сертификатов разработчика) и на *каких* устройствах можно установить приложение.

Чтобы вручную создать профиль подготовки для разработки, выполните указанные ниже действия:

1. В браузере Safari перейдите в [Apple Developers Member Center](https://developer.apple.com/membercenter/index.action) и в разделе *Certificates, Identifiers & Profiles* (Сертификаты, идентификаторы и профили) выберите элемент Provisioning Profiles (Профили подготовки).
2. Чтобы создать профиль, в правом верхнем углу нажмите кнопку **+**.
3. В разделе **Development** (Разработка) установите переключатель в положение **iOS App Development** (Разработка приложений для iOS) и нажмите кнопку **Continue** (Продолжить).

    [![](manual-provisioning-images/provisioning-profile01.png "Выберите тип создаваемого профиля")](manual-provisioning-images/provisioning-profile01.png#lightbox)
4. В раскрывающемся меню выберите нужный идентификатор приложения.

    [![](manual-provisioning-images/provisioning-profile02.png "Выберите нужный идентификатор приложения")](manual-provisioning-images/provisioning-profile02.png#lightbox)
5. Выберите сертификаты, которые нужно включить в профиль подготовки, и нажмите кнопку **Continue** (Продолжить):

    [![](manual-provisioning-images/provisioning-profile03.png "Выберите сертификаты, которые нужно включить в профиль подготовки")](manual-provisioning-images/provisioning-profile03.png#lightbox)
6. Выберите все устройства, на которых будет устанавливаться приложение.

    [![](manual-provisioning-images/provisioning-profile04.png "Выберите все устройства, на которых будет устанавливаться приложение")](manual-provisioning-images/provisioning-profile04.png#lightbox)
7. Укажите имя, по которому можно определить профиль подготовки, и нажмите кнопку **Continue** (Продолжить), чтобы создать профиль:

    [![](manual-provisioning-images/provisioning-profile05.png "Укажите имя, по которому можно определить профиль подготовки")](manual-provisioning-images/provisioning-profile05.png#lightbox)
8. Чтобы скачать профиль подготовки на компьютер Mac, нажмите кнопку **Download** (Скачать):

    [![](manual-provisioning-images/provisioning-profile06.png "Скачивание профиля подготовки")](manual-provisioning-images/provisioning-profile06.png#lightbox)
9. Дважды щелкните файл, чтобы установить профиль подготовки в Xcode. Имейте в виду, что в Xcode может не быть никаких визуальных указаний на то, что профиль установился. Проверить это можно путем перехода в раздел **Xcode > Preferences > Accounts** (Xcode > Настройки > Учетные записи). Выберите свой идентификатор Apple и щелкните **View Details...** (Показать подробности...). Новый профиль подготовки должен присутствовать в списке, как показано ниже:

      [![](manual-provisioning-images/provisioning-profile07.png "Просмотр профиля в Xcode")](manual-provisioning-images/provisioning-profile07.png#lightbox)

После успешного создания профиля подготовки может потребоваться обновить Xcode, чтобы все сертификаты разработки стали доступны для Visual Studio для Mac и Visual Studio.

<a name="download" />

## <a name="downloading-profiles-and-certificates-in-xcode"></a>Скачивание профилей и сертификатов в Xcode

Сертификаты и профили подготовки, созданные на портале разработчика Apple, могут не отображаться в Xcode автоматически. Поэтому их может потребоваться скачать, чтобы они стали доступны в Visual Studio для Mac и Visual Studio. Чтобы обновить и скачать сертификаты, созданные на портале разработчика Apple, выполните указанные ниже действия:

1.   Выйдите из Visual Studio для Mac или Visual Studio.
2.   Запустите Xcode.
3.   Выберите **Xcode Menu > Preferences...** (Меню Xcode > Предпочтения...).
4.   Перейдите на вкладку **Accounts** (Учетные записи).
5.   Выберите команду и нажмите кнопку **Скачать профили вручную**: [![](manual-provisioning-images/selectteam1.png "Скачивание профилей вручную")](manual-provisioning-images/selectteam1.png#lightbox)

6.   Выйдите из Xcode.
7.  Запустите Visual Studio для Mac или Visual Studio.

Новые сертификаты или профили подготовки станут доступны для использования в Visual Studio для Mac или Visual Studio.

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio для Mac](#tab/macos)

> [!IMPORTANT]
> Чтобы сертификаты или профили, созданные или измененные в Xcode, стали доступны в среде Visual Studio для Mac, ее нужно закрыть и перезапустить.

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

> [!IMPORTANT]
> Чтобы сертификаты или профили, созданные или измененные в Xcode, стали доступны в среде Visual Studio, ее нужно закрыть и перезапустить.

-----

<a name="appservices" />

## <a name="provisioning-for-application-services"></a>Подготовка служб приложений

Apple предоставляет ряд специальных служб приложений, также называемых возможностями, которые можно активировать для приложений Xamarin.iOS. Эти службы необходимо настроить как на портале подготовки iOS при создании **идентификатора приложения**, так и в файле **Entitlements.plist**, входящем в проект приложения Xamarin.iOS. Сведения о добавлении служб приложений к приложению см. в руководствах [Работа с возможностями](~/ios/deploy-test/provisioning/capabilities/index.md) и [Работа с назначениями](~/ios/deploy-test/provisioning/entitlements.md).

* Создайте идентификатор приложения с требуемыми службами приложений.
* Создайте [профиль подготовки](#provisioningprofile), содержащий этот идентификатор приложения.
* Задайте назначения в проекте Xamarin.iOS

## <a name="deploying-to-a-device"></a>Развертывание на устройстве

На этом этапе подготовка должна быть завершена, а приложение готово к развертыванию на устройстве. Выполните указанные ниже действия:

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio для Mac](#tab/macos)

> [!IMPORTANT]
> Прежде чем начать, убедитесь, что в файле **Info.plist** выбран параметр **Manual Provisioning** (Подготовка вручную).

1. Подключите устройство к компьютеру Mac.
2. В файле **Info.plist** проекта проверьте, соответствует ли идентификатор пакета идентификатору приложения (если только не используется шаблон идентификатора приложения):

  ![](manual-provisioning-images/deploydevice01xs.png "Ввод идентификатора")

3. Щелкните проект правой кнопкой мыши, откройте диалоговое окно "Параметры проекта" и перейдите на страницу **Сборка > Подписывание пакета iOS**. В раскрывающихся списках **Удостоверение подписывания** и **Профиль подготовки** убедитесь в том, что в Visual Studio для Mac доступны соответствующие профили, а затем выберите определенное удостоверение и профиль:

  ![](manual-provisioning-images/deploydevice02xs.png "Выбор удостоверения и профиля")

Если выбрано значение **Автоматически**, среда Visual Studio для Mac выберет удостоверение и профиль в соответствии с идентификатором пакета, заданным в шаге 2.

4. В качестве конфигурации сборки должно быть выбрано значение **iPhone** / **iPad**, а не симулятор.
5. В Visual Studio для Mac нажмите кнопку **Запуск**. Приложение должно запуститься на устройстве.

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

> [!IMPORTANT]
> Для начала выберите схему **Подготовка вручную** в разделе **Проект > Свойства подготовки…**.

1. Подключите устройство к узлу сборки Mac.
2. В файле **Info.plist** проекта проверьте, соответствует ли идентификатор пакета идентификатору приложения:

  ![](manual-provisioning-images/servicevs01.png "Ввод идентификатора")

3. Щелкните проект правой кнопкой мыши, откройте диалоговое окно "Параметры проекта" и перейдите на страницу **Сборка > Подписывание пакета iOS**. В раскрывающихся списках **Удостоверение подписывания** и **Профиль подготовки** убедитесь в том, что в Visual Studio доступны соответствующие профили, а затем выберите определенное удостоверение и профиль.

    Если выбрано значение **Автоматически**, среда Visual Studio выберет удостоверение и профиль в соответствии с идентификатором пакета, заданным в шаге 2.

4. В качестве конфигурации сборки должно быть выбрано значение **iPhone** или **iPad**, а не симулятор.
5. В Visual Studio нажмите кнопку **Запуск**. Приложение должно запуститься на устройстве.


-----

## <a name="summary"></a>Сводка

В этом руководстве были рассмотрены действия по настройке среды разработки для Xamarin.iOS. Вы узнали, как код приложения подписывается с использованием сведений о разработчике, его команде и устройствах, на которых может выполняться приложение, а также уникального идентификатора приложения.

## <a name="related-links"></a>Связанные ссылки

- [Бесплатная подготовка](~/ios/get-started/installation/device-provisioning/free-provisioning.md)
- [Распространение приложений](~/ios/deploy-test/app-distribution/index.md)
- [Устранение неполадок](~/ios/deploy-test/troubleshooting.md)
- [Руководство Apple. Распространение приложений](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html)
