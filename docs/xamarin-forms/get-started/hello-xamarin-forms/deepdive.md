---
title: Подробное знакомство с Xamarin.Forms
description: Эта статья содержит общие сведения о разработке приложений с использованием Xamarin.Forms. Помимо прочего, здесь описываются структура приложения Xamarin.Forms и принципы его работы, а также пользовательский интерфейс.
ms.topic: quickstart
ms.prod: xamarin
ms.assetid: d97aa580-1eb9-48b3-b15b-0d7421ea7ae
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 06/13/2018
ms.openlocfilehash: 7eff7f4413b533caadcf2aa8b5eed8c4ab65449d
ms.sourcegitcommit: b56b3f906d2c05a3f1be219ef41be8b79e519b8e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/25/2018
ms.locfileid: "39242229"
---
# <a name="xamarinforms-deep-dive"></a>Подробное знакомство с Xamarin.Forms

В [кратком руководстве по Xamarin.Forms](~/xamarin-forms/get-started/hello-xamarin-forms/quickstart.md) было построено приложение Phoneword. В этой статье выполняется проверка созданных компонентов, позволяющая получить представление об основных принципах работы приложений Xamarin.Forms.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

## <a name="introduction-to-visual-studio"></a>Введение в Visual Studio

Visual Studio — это полнофункциональная интегрированная среда разработки (IDE) от корпорации Майкрософт. Она включает в себя полностью интегрированный визуальный конструктор, текстовый редактор с инструментами рефакторинга, обозреватель сборок, средства интеграции исходного кода и другие возможности. В этой статье описывается использование некоторых основных возможностей Visual Studio с помощью подключаемого модуля Xamarin.

Код в Visual Studio упорядочен по *решениям* и *проектам*. Решение — это контейнер для одного или нескольких проектов. Проект может представлять собой приложение, вспомогательную библиотеку, тестовое приложение и т. д. Приложение Phoneword включает в себя одно решение, содержащее четыре проекта, как показано на следующем снимке экрана.

![](deepdive-images/vs/solution.png "Обозреватель решений Visual Studio")

Решение содержит следующие проекты:

- Phoneword — это проект библиотеки .NET Standard, который содержит весь общий код и общий пользовательский интерфейс.
- Phoneword.Android — этот проект содержит код для Android и представляет собой точку входа для приложения Android.
- Phoneword.iOS — этот проект содержит код для iOS и представляет собой точку входа для приложения iOS.
- Phoneword.UWP — этот проект содержит код для универсальной платформы Windows (UWP) и представляет собой точку входа для приложения UWP.

## <a name="anatomy-of-a-xamarinforms-application"></a>Структура приложения Xamarin.Forms

На следующих снимках экрана показано содержимое проекта библиотеки .NET Standard Phoneword в Visual Studio для Mac:

![](deepdive-images/vs/net-standard-project.png "Содержимое проекта .NET Standard Phoneword")

В этом проекте есть узел **Зависимости**, который содержит узлы **NuGet** и **SDK**. Узел **NuGet** содержит добавленный в проект пакет Xamarin.Forms NuGet, а узел **SDK** содержит метапакет `NETStandard.Library`, который ссылается на полный набор пакетов NuGet, определяющих .NET Standard.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

## <a name="introduction-to-visual-studio-for-mac"></a>Введение в Visual Studio для Mac

Visual Studio для Mac — это бесплатная интегрированная среда разработки (IDE) с открытым кодом, похожая на Visual Studio. Она включает в себя полностью интегрированный визуальный конструктор, текстовый редактор с инструментами рефакторинга, обозреватель сборок, средства интеграции исходного кода и другие возможности. Дополнительные сведения о Visual Studio для Mac см. в разделе [Знакомство с Visual Studio для Mac](/visualstudio/mac/).

В Visual Studio для Mac, так же как в Visual Studio, код упорядочивается по *решениям* и *проектам*. Решение — это контейнер для одного или нескольких проектов. Проект может представлять собой приложение, вспомогательную библиотеку, тестовое приложение и т. д. Приложение Phoneword включает в себя одно решение, содержащее три проекта, как показано на следующем снимке экрана.

![](deepdive-images/xs/solution.png "Область решений в Visual Studio для Mac")

Решение содержит следующие проекты:

- Phoneword — это проект библиотеки .NET Standard, который содержит весь общий код и общий пользовательский интерфейс.
- Phoneword.Droid — этот проект содержит код для Android и представляет собой точку входа для приложений Android.
- Phoneword.iOS — этот проект содержит код для iOS и представляет собой точку входа для приложений iOS.

## <a name="anatomy-of-a-xamarinforms-application"></a>Структура приложения Xamarin.Forms

На следующих снимках экрана показано содержимое проекта библиотеки .NET Standard Phoneword в Visual Studio для Mac:

![](deepdive-images/xs/library-project.png "Содержимое проекта библиотеки .NET Standard Phoneword")

В этом проекте есть узел **Зависимости**, который содержит узлы **NuGet** и **SDK**. Узел **NuGet** содержит добавленный в проект пакет Xamarin.Forms NuGet, а узел **SDK** содержит метапакет `NETStandard.Library`, который ссылается на полный набор пакетов NuGet, определяющих .NET Standard.

-----

Проект также состоит из нескольких файлов:

- **App.xaml** — разметка XAML для класса `App`, который определяет словарь ресурсов для приложения.
- **App.xaml.cs** — код программной части для класса `App`, который обеспечивает создание экземпляра первой страницы, отображаемой приложением на каждой платформе, а также обработку событий жизненного цикла приложения.
- **IDialer.cs** — интерфейс `IDialer`, который указывает, что в любом реализующем классе должен быть предоставлен метод `Dial`.
- **MainPage.xaml** — разметка XAML для класса `MainPage`, который определяет пользовательский интерфейс страницы, отображаемой при запуске приложения.
- **MainPage.xaml.cs** — код программной части для класса `MainPage`, который содержит бизнес-логику, выполняемую при взаимодействии пользователя со страницей.
- **PhoneTranslator.cs** — бизнес-логика, отвечающая за преобразования номера телефона из текстового в цифровой формат. Вызывается из файла **MainPage.xaml.cs**.

Дополнительные сведения о структуре приложения Xamarin.iOS см. [здесь](~/ios/get-started/hello-ios/hello-ios-deepdive.md#anatomy-of-a-xamarinios-application). Дополнительные сведения о структуре приложения Xamarin.Android см. [здесь](~/android/get-started/hello-android/hello-android-deepdive.md#anatomy).

## <a name="architecture-and-application-fundamentals"></a>Архитектура и принципы работы приложения

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

По своей архитектуре приложения Xamarin.Forms не отличаются от традиционных кроссплатформенных приложений. Общий код обычно помещается в библиотеку .NET Standard и используется приложениями для конкретных платформ. На следующей схеме показаны эти взаимосвязи для приложения Phoneword:

![](deepdive-images/vs/architecture.png "Архитектура приложения Phoneword")

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

По своей архитектуре приложения Xamarin.Forms не отличаются от традиционных кроссплатформенных приложений. Общий код обычно помещается в библиотеку .NET Standard и используется приложениями для конкретных платформ. На следующей схеме показаны эти взаимосвязи для приложения Phoneword:

![](deepdive-images/xs/architecture.png "Архитектура приложения Phoneword")

-----

Чтобы код запуска как можно больше использовался повторно, в приложениях Xamarin.Forms есть отдельный класс `App`, который отвечает за создание экземпляра первой страницы, отображаемой приложением на каждой платформе, как показано в следующем примере кода:

```csharp
using Xamarin.Forms;
using Xamarin.Forms.Xaml;

[assembly: XamlCompilation(XamlCompilationOptions.Compile)]
namespace Phoneword
{
    public partial class App : Application
    {
        public App()
        {
            InitializeComponent();
            MainPage = new MainPage();
        }
        ...
    }
}
```

Этот код присваивает свойству `MainPage` класса `App` в качестве значения новый экземпляр класса [`MainPage`](xref:Xamarin.Forms.Application.MainPage). Кроме того, атрибут [`XamlCompilation`](xref:Xamarin.Forms.Xaml.XamlCompilationAttribute) включает компилятор XAML, что позволяет компилировать код XAML непосредственно в промежуточный язык. Дополнительные сведения см. в разделе [Компиляция XAML](~/xamarin-forms/xaml/xamlc.md).

## <a name="launching-the-application-on-each-platform"></a>Запуск приложения на каждой платформе

### <a name="ios"></a>iOS

Для запуска начальной страницы Xamarin.Forms в iOS проект Phoneword.iOS включает в себя класс `AppDelegate`, который наследуется от класса `FormsApplicationDelegate`, как показано в следующем примере кода:

```csharp
namespace Phoneword.iOS
{
    [Register ("AppDelegate")]
    public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
    {
        public override bool FinishedLaunching (UIApplication app, NSDictionary options)
        {
            global::Xamarin.Forms.Forms.Init ();
            LoadApplication (new App ());
            return base.FinishedLaunching (app, options);
        }
    }
}
```

Переопределение `FinishedLaunching` инициализирует платформу Xamarin.Forms, вызывая метод `Init`. В результате реализация Xamarin.Forms для iOS загружается в приложении, прежде чем корневой контроллер представления задается путем вызова метода `LoadApplication`.

### <a name="android"></a>Android

Чтобы начальную страницу Xamarin.Forms можно было запустить в Android, проект Phoneword.Droid включает код, который создает действие `Activity` с атрибутом `MainLauncher`, которое наследует от класса `FormsAppCompatActivity`, как показано в следующем примере кода:

```csharp
namespace Phoneword.Droid
{
    [Activity(Label = "Phoneword", 
              Icon = "@mipmap/icon", 
              Theme = "@style/MainTheme", 
              MainLauncher = true,
              ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation)]
    public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
    {
        internal static MainActivity Instance { get; private set; }

        protected override void OnCreate(Bundle bundle)
        {
            TabLayoutResource = Resource.Layout.Tabbar;
            ToolbarResource = Resource.Layout.Toolbar;

            base.OnCreate(bundle);
            Instance = this;
            global::Xamarin.Forms.Forms.Init(this, bundle);
            LoadApplication(new App());
        }
    }
}
```

Переопределение `OnCreate` инициализирует платформу Xamarin.Forms, вызывая метод `Init`. В результате реализация Xamarin.Forms для Android загружается в приложении перед загрузкой самого приложения Xamarin.Forms. Кроме того, класс `MainActivity` хранит ссылку на себя в свойстве `Instance`. Свойство `Instance` именуется локальным контекстом и на него ссылается класс `PhoneDialer`.

## <a name="universal-windows-platform"></a>Универсальная платформа Windows 

В приложениях универсальной платформы Windows (UWP) метод `Init`, который инициализирует платформу Xamarin.Forms, вызывается из класса `App`:

```csharp
Xamarin.Forms.Forms.Init (e);

if (e.PreviousExecutionState == ApplicationExecutionState.Terminated)
{
  ...
}
```

В результате в приложении загружается реализация Xamarin.Forms для UWP. Начальная страница Xamarin.Forms запускается классом `MainPage`, как показано в следующем примере кода:

```csharp
namespace Phoneword.UWP
{
    public sealed partial class MainPage
    {
        public MainPage()
        {
            this.InitializeComponent();
            this.LoadApplication(new Phoneword.App());
        }
    }
}
```

Приложение Xamarin.Forms загружается с помощью метода `LoadApplication`.

> [!NOTE]
> Приложения для универсальной платформы Windows (UWP) можно создавать с помощью Xamarin.Forms, однако использовать при этом можно только Visual Studio для Windows.

## <a name="user-interface"></a>Пользовательский интерфейс

Для создания пользовательского интерфейса приложения Xamarin.Forms используются четыре основные группы элементов управления.

1. **Страницы** — страницы Xamarin.Forms представляют экраны в кроссплатформенных мобильных приложениях. В приложении Phoneword для отображения отдельного экрана используется класс [`ContentPage`](xref:Xamarin.Forms.ContentPage). Дополнительные сведения о страницах см. в статье [Страницы Xamarin.Forms](~/xamarin-forms/user-interface/controls/pages.md).
1. **Макеты** — макеты Xamarin.Forms представляют собой контейнеры, которые служат для объединения представлений в логические структуры. В приложении Phoneword для упорядочения элементов управления в горизонтальный стек используется класс [`StackLayout`](xref:Xamarin.Forms.StackLayout). Дополнительные сведения о макетах см. в статье [Макеты Xamarin.Forms](~/xamarin-forms/user-interface/controls/layouts.md).
1. **Представления** — представления Xamarin.Forms являются элементами управления, отображаемыми в пользовательском интерфейсе, например метки, кнопки и поля ввода текста. В приложении Phoneword используются элементы управления [`Label`](xref:Xamarin.Forms.Label), [`Entry`](xref:Xamarin.Forms.Entry) и [`Button`](xref:Xamarin.Forms.Button). Дополнительные сведения о представлениях см. в статье [Представления Xamarin.Forms](~/xamarin-forms/user-interface/controls/views.md).
1. **Ячейки** — ячейки Xamarin.Forms являются специальными объектами, представляющими элементы списка и описывающими способ их отрисовки. В приложении Phoneword ячейки не используются. Дополнительные сведения о ячейках см. в статье [Ячейки Xamarin.Forms](~/xamarin-forms/user-interface/controls/cells.md).

Во время выполнения каждый элемент управления сопоставляется с собственным аналогом, который и будет отрисовываться.

При выполнении приложения Phoneword на любой платформе отображается один экран, который соответствует [`Page`](xref:Xamarin.Forms.Page) в Xamarin.Forms. Класс `Page` представляет *ViewGroup* в Android, *контроллер представления* в iOS или *страницу* на универсальной платформе Windows. Приложение Phoneword также создает экземпляр объекта [`ContentPage`](xref:Xamarin.Forms.ContentPage), представляющий класс `MainPage`, разметка XAML которого показана в следующем примере кода:

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
                         xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                         x:Class="Phoneword.MainPage">
        ...
        <StackLayout>
            <Label Text="Enter a Phoneword:" />
            <Entry x:Name="phoneNumberText" Text="1-855-XAMARIN" />
            <Button x:Name="translateButon" Text="Translate" Clicked="OnTranslate" />
            <Button x:Name="callButton" Text="Call" IsEnabled="false" Clicked="OnCall" />
        </StackLayout>
</ContentPage>
```

Класс `MainPage` использует элемент управления [`StackLayout`](xref:Xamarin.Forms.StackLayout) для автоматического упорядочения элементов управления на экране независимо от размера экрана. Дочерние элементы размещаются поочередно по вертикали в порядке добавления. Элемент управления `StackLayout` содержит элементы управления [`Label`](xref:Xamarin.Forms.Label) (отображает текст на странице), [`Entry`](xref:Xamarin.Forms.Entry) (принимает вводимый пользователем текст), а также два элемента управления [`Button`](xref:Xamarin.Forms.Button) (используются для выполнения кода в ответ на события касания).

Дополнительные сведения о XAML в Xamarin.Forms см. в разделе [Основы XAML в Xamarin.Forms](~/xamarin-forms/xaml/xaml-basics/index.md).

### <a name="responding-to-user-interaction"></a>Реакция на действия пользователей

Объект, определенный в XAML, может инициировать событие, которое обрабатывается в файле кода программной части. В следующем примере кода показан метод `OnTranslate` в коде программной части для класса `MainPage`, который выполняется в ответ на событие [`Clicked`](xref:Xamarin.Forms.Button.Clicked), инициируемое при нажатии кнопки *Translate* (Преобразовать).

```csharp
void OnTranslate(object sender, EventArgs e)
{
    translatedNumber = Core.PhonewordTranslator.ToNumber (phoneNumberText.Text);
    if (!string.IsNullOrWhiteSpace (translatedNumber)) {
        callButton.IsEnabled = true;
        callButton.Text = "Call " + translatedNumber;
    } else {
        callButton.IsEnabled = false;
        callButton.Text = "Call";
    }
}
```

Метод `OnTranslate` преобразует номер телефона из текстового формата в цифровой и в ответ задает свойства кнопки звонка. Файл кода программной части для класса XAML может получать доступ к объекту, определенному в XAML, по имени, которое назначено ему в атрибуте `x:Name`. Значение, присваиваемое этому атрибуту, должно соответствовать правилам C# в отношении переменных, то есть должно начинаться с буквы или знака подчеркивания и не содержать внутренних пробелов.

Привязка кнопки преобразования к методу `OnTranslate` выполняется в разметке XAML для класса `MainPage`:

```xaml
<Button x:Name="translateButon" Text="Translate" Clicked="OnTranslate" />
```

## <a name="additional-concepts-introduced-in-phoneword"></a>Дополнительные понятия, представленные в Phoneword

В приложении Phoneword для Xamarin.Forms представлено несколько понятий, не охваченных этой статьей. В их число входят следующие:

- Включение и отключение кнопок. Чтобы включить или отключить объект [`Button`](xref:Xamarin.Forms.Button), необходимо изменить его свойство [`IsEnabled`](xref:Xamarin.Forms.VisualElement.IsEnabled). Например, в следующем примере кода отключается объект `callButton`:

    ```csharp
    callButton.IsEnabled = false;
    ```

- Отображение диалогового окна оповещения. Когда пользователь нажимает **кнопку звонка**, приложение Phoneword отображает *диалоговое окно оповещения*, в котором можно выполнить или отменить звонок. Для создания этого диалогового окна используется метод [`DisplayAlert`](xref:Xamarin.Forms.Page.DisplayAlert(System.String,System.String,System.String,System.String)), как показано в следующем примере кода:

    ```csharp
    await this.DisplayAlert (
            "Dial a Number",
            "Would you like to call " + translatedNumber + "?",
            "Yes",
            "No");
    ```

- Доступ к собственным функциям осуществляется с помощью класса [`DependencyService`](xref:Xamarin.Forms.DependencyService). В приложении Phoneword используется класс `DependencyService`, который разрешает интерфейс `IDialer` для реализации набора номера телефона в соответствии с конкретной платформой, как показано в следующем примере кода из проекта Phoneword:

    ```csharp
    async void OnCall (object sender, EventArgs e)
    {
        ...
        var dialer = DependencyService.Get<IDialer> ();
        ...
    }
    ```

  Дополнительные сведения о классе [`DependencyService`](xref:Xamarin.Forms.DependencyService) см. в разделе [Доступ к собственным функциям через DependencyService](~/xamarin-forms/app-fundamentals/dependency-service/index.md).

- Выполнение телефонного звонка по URL-адресу. Приложение Phoneword использует метод `OpenURL` для запуска системного приложения телефона. URL-адрес состоит из префикса `tel:` и вызываемого номера телефона, как показано в следующем примере кода для проекта iOS:

    ```csharp
    return UIApplication.SharedApplication.OpenUrl (new NSUrl ("tel:" + number));
    ```

- Настройка параметров макета платформы. С помощью класса [`Device`](xref:Xamarin.Forms.Device) разработчики могут настраивать макет и функции приложений для отдельных платформ. Это показано в следующем примере кода, в котором на разных платформах используются разные значения [`Padding`](xref:Xamarin.Forms.Layout.Padding) для корректного отображения каждой страницы:

    ```xaml
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms" ... >
        <ContentPage.Padding>
            <OnPlatform x:TypeArguments="Thickness">
                <On Platform="iOS" Value="20, 40, 20, 20" />
                <On Platform="Android, UWP" Value="20" />
            </OnPlatform>
        </ContentPage.Padding>
        ...
    </ContentPage>
    ```

  Дополнительные сведения о настройке параметров платформы см. в разделе [Класс Device](~/xamarin-forms/platform/device.md).

## <a name="testing-and-deployment"></a>Тестирование и развертывание

Как Visual Studio для Mac, так и Visual Studio предоставляют множество возможностей для тестирования и развертывания приложения. Одной из неотъемлемых стадий жизненного цикла приложения является отладка, которая позволяет выявить проблемы в коде. Дополнительные сведения см. в разделах [Установка точки останова](https://github.com/xamarin/recipes/tree/master/Recipes/cross-platform/ide/debugging/set_a_breakpoint), [Пошаговая отладка кода](https://github.com/xamarin/recipes/tree/master/Recipes/cross-platform/ide/debugging/step_through_code) и [Вывод данных в окно журнала](https://github.com/xamarin/recipes/tree/master/Recipes/cross-platform/ide/debugging/output_information_to_log_window).

Симуляторы позволяют начать тестирование и развертывание приложения, реализуя полезные функции для тестирования приложений. Тем не менее пользователи будут работать с готовым приложением не в симуляторе, поэтому любое приложение необходимо тестировать на реальных устройствах как можно раньше и чаще. Дополнительные сведения о процессе подготовки для устройств iOS см. в разделе [Подготовка устройства](~/ios/get-started/installation/device-provisioning/index.md). Дополнительные сведения о процессе подготовки для устройств Android см. в разделе [Настройка устройства для разработки](~/android/get-started/installation/set-up-device-for-development.md).

## <a name="summary"></a>Сводка

В этой статье приводятся общие сведения о разработке приложений с использованием Xamarin.Forms. Помимо прочего, здесь описываются структура приложения Xamarin.Forms и принципы его работы, а также пользовательский интерфейс.

В следующем разделе этого руководства мы рассмотрим дополнительные понятия и функции архитектуры Xamarin.Forms и расширим возможности приложения, включив для него несколько экранов.
