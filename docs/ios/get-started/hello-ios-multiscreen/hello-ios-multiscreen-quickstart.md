---
title: 'Привет, iOS (несколько экранов): краткое руководство'
description: Этот документ показывает, как развернуть пример приложения Phoneword для добавления второго экрана, параллельно знакомя читателя со структурой модель-представление-контроллер (MVC), навигацией iOS и другими ключевыми концепциями по разработке для iOS.
ms.topic: quickstart
ms.prod: xamarin
ms.assetid: d72e6230-c9ee-4bee-90ec-877d256821aa
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 12/02/2016
ms.openlocfilehash: 469032dc7caa46c6a89b350dc37bc9a93366066a
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34785675"
---
# <a name="hello-ios-multiscreen--quickstart"></a>Привет, iOS (несколько экранов): краткое руководство

В этой части пошагового руководства вы добавите второй экран для приложения Phoneword, отображающего журнал телефонных номеров, на которые выполнялись вызовы из приложения. Итоговое приложение будет иметь второй экран с журналом вызовов, как показано на следующем снимке экрана:

 [![](hello-ios-multiscreen-quickstart-images/00.png "Итоговое приложение будет иметь второй экран с журналом вызовов, как показано на снимке экрана")](hello-ios-multiscreen-quickstart-images/00.png#lightbox)

Прилагаемый [подробный обзор](~/ios/get-started/hello-ios-multiscreen/hello-ios-multiscreen-deepdive.md) описывает полученное приложение, а также затрагивает архитектуру, навигацию и другие новые понятия iOS, которые вам встретились.

 <a name="Requirements" />

## <a name="requirements"></a>Требования

Это руководство начинается с того момента, на котором заканчивается документ "Привет, iOS", поэтому вам нужно сначала изучить [Привет, iOS: краткое руководство](~/ios/get-started/hello-ios/index.md). Готовую версию приложения Phoneword можно скачать из примера [Привет, iOS](https://developer.xamarin.com/samples/monotouch/Hello_iOS/).

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

## <a name="walkthrough"></a>Пошаговое руководство

В этом пошаговом руководстве вы добавите в приложение **Phoneword** экран "Call History" (Журнал вызовов).


1. Откройте приложение **Phoneword** в Visual Studio для Mac. При необходимости готовое приложение Phoneword из пошагового руководства [Привет, iOS](~/ios/get-started/hello-ios/index.md) можно скачать [здесь](https://developer.xamarin.com/samples/monotouch/Hello_iOS/).


2. Откройте файл **Main.storyboard** из **Панели решения**:

  ![](hello-ios-multiscreen-quickstart-images/02new.png "Файл Main.storyboard в конструкторе iOS")


3. Перетащите **контроллер навигации** из **панели элементов** в область конструктора (чтобы уместить все элементы в этой области, может потребоваться уменьшить масштаб):

  ![](hello-ios-multiscreen-quickstart-images/03new.png "Перетаскивание контроллера навигации из панели элементов в область конструктора")


4. Перетащите элемент **Sourceless Segue** (Переход без источника) (это серая стрелка слева от контроллера представления) в **контроллер навигации**, чтобы изменить начальную точку приложения:

  ![](hello-ios-multiscreen-quickstart-images/04new.png "Перетаскивание перехода без источника на контроллер навигации для изменения начальной точки приложения")


5. Выберите существующий **контроллер корневого представления**, щелкнув нижнюю полосу, а затем нажмите клавишу **DELETE**, чтобы удалить его из области конструктора.
Переместите сцену **Phoneword** к **контроллеру навигации**:

  ![](hello-ios-multiscreen-quickstart-images/05new.png "Перемещение сцены Phoneword к контроллеру навигации")


6. Задайте **ViewController** в качестве **контроллера корневого представления** у контроллера навигации. Нажмите и удерживайте клавишу **CTRL** и щелкните внутри **контроллера навигации**. Должна появиться синяя линия. Затем, продолжая удерживать клавишу **CTRL**, перетащите элементы из **контроллера навигации** в сцену **Phoneword**. Это называется _перетаскиванием с удержанием клавиши CTRL_:

 ![](hello-ios-multiscreen-quickstart-images/06.png "Перетаскивание элементов из контроллера навигации в сцену Phoneword")


7. В контекстном меню задайте связь **Корень**:

  ![](hello-ios-multiscreen-quickstart-images/07new.png "Задание связи \"Корень\"")

  Теперь **ViewController является** контроллером корневого представления контроллера навигации **:** 

  ![](hello-ios-multiscreen-quickstart-images/08.png "Теперь ViewController является контроллером корневого представления у контроллера навигации")


8. Дважды щелкните **Phoneword** экрана **заголовок** панели и изменить **заголовок** для **Phoneword**:

  ![](hello-ios-multiscreen-quickstart-images/09.png "Изменение заголовка на Phoneword")


9. Перетащите элемент **Button** из **панели элементов** и поместите его под элементом **Call Button** (Кнопка вызова). Перетащите маркеры, чтобы сделать новый элемент **Button** такой же ширины, что и элемент **Call Button** (Кнопка вызова):

  ![](hello-ios-multiscreen-quickstart-images/10new.png "Сделайте новый элемент \"Button\" такой же ширины, что и элемент \"Call Button\" (Кнопка вызова)")


10. На **Панели свойств** измените **имя** кнопки на **CallHistoryButton**, а **заголовок** — на **Call History**:

  ![](hello-ios-multiscreen-quickstart-images/11new.png "Измените \"Имя\" с \"Button\" на \"CallHistoryButton\" и измените \"Заголовок\" на \"Call History\" (Журнал вызовов)")


11. Создайте экран **Call History** (Журнал вызовов). Перетащите **контроллер представления таблиц** из **панели элементов** в область конструктора:

 ![](hello-ios-multiscreen-quickstart-images/12new.png "Перетащите контроллер представления таблиц в область конструктора")


12. Затем выберите **контроллер представления таблиц**, щелкнув черную полосу в нижней части сцены. На **Панели свойств** измените класс **контроллера представления таблиц** на `CallHistoryController` и нажмите клавишу **ВВОД**:

  ![](hello-ios-multiscreen-quickstart-images/13new.png "Измените класс контроллеров представления таблицы на CallHistoryController")

  Конструктор IOS создает пользовательский резервный класс `CallHistoryController` для управления иерархией представлений содержимого на этом экране.
  На **Панели решения** появляется файл **CallHistoryController.cs**:

  ![](hello-ios-multiscreen-quickstart-images/14new.png "Файл CallHistoryController.cs на Панели решения")


13. Дважды щелкните файл **CallHistoryController.cs**, чтобы открыть его, и замените содержимое следующим кодом:

  ```csharp
  using System;
  using Foundation;
  using UIKit;
  using System.Collections.Generic;

  namespace Phoneword_iOS
  {
      public partial class CallHistoryController : UITableViewController
      {
          public List<string> PhoneNumbers { get; set; }

          static NSString callHistoryCellId = new NSString ("CallHistoryCell");

          public CallHistoryController (IntPtr handle) : base (handle)
          {
              TableView.RegisterClassForCellReuse (typeof(UITableViewCell), callHistoryCellId);
              TableView.Source = new CallHistoryDataSource (this);
              PhoneNumbers = new List<string> ();
          }

          class CallHistoryDataSource : UITableViewSource
          {
              CallHistoryController controller;

              public CallHistoryDataSource (CallHistoryController controller)
              {
                  this.controller = controller;
              }

              public override nint RowsInSection (UITableView tableView, nint section)
              {
                  return controller.PhoneNumbers.Count;
              }

              public override UITableViewCell GetCell (UITableView tableView, NSIndexPath indexPath)
              {
                  var cell = tableView.DequeueReusableCell (CallHistoryController.callHistoryCellId);

                  int row = indexPath.Row;
                  cell.TextLabel.Text = controller.PhoneNumbers [row];
                  return cell;
              }
          }
      }
  }
  ```

  Сохраните приложение (**⌘+S**) и выполните его сборку (**⌘+B**), чтобы убедиться в отсутствии ошибок.


14. Создайте _переход_ между сценой **Phoneword** и сценой **Call History** (Журнал вызовов).
  В **сцене Phoneword** выберите **Call History Button** (Кнопка журнала вызовов) и, удерживая нажатой клавишу CTRL, перетащите из элемента **Button** в сцену **Call History** (Журнал вызовов):

  ![](hello-ios-multiscreen-quickstart-images/15.png "Удерживая нажатой клавишу CTRL, перетащите из элемента \"Button\" в сцену \"Call History\" (Журнал вызовов)")

  В контекстном меню **Action Segue** (Переход между действиями) выберите **Показать**.

  Конструктор iOS добавляет переход между двумя сценами:

  ![](hello-ios-multiscreen-quickstart-images/17new.png "Переход между двумя сценами")


15. Добавьте **Заголовок** в **контроллер представления таблиц**, выбрав черную полосу в нижней части сцены и изменив **Контроллер представления > Заголовок** на **Call History** (Журнал вызовов) на **Панели свойств**:

  ![](hello-ios-multiscreen-quickstart-images/18new.png "Изменение значения \"Контроллер представления > Заголовок\" на \"Call History\" (Журнал вызовов) на Панели свойств")

16. При запуске приложения **Call History Button** (Кнопка журнала вызовов) откроет экран **Call History** (Журнал вызовов), однако представление таблиц будет пустым, так как отсутствует код для отслеживания и отображения телефонных номеров.

  Это приложение сохраняет телефонные номера в виде списка строк.

  Добавьте директиву `using` для `System.Collections.Generic` в начало **ViewController**:

  ```csharp
  using System.Collections.Generic;
  ```



17. Измените класс `ViewController` с помощью следующего кода:

    ```csharp
    using System;
    using System.Collections.Generic;
    using Foundation;
    using UIKit;

    namespace Phoneword_iOS
    {
      public partial class ViewController : UIViewController
      {
        string translatedNumber = "";

        public List<string> PhoneNumbers { get; set; }

        protected ViewController(IntPtr handle) : base(handle)
        {
          //initialize list of phone numbers called for Call History screen
          PhoneNumbers = new List<string>();
        }

        public override void ViewDidLoad()
        {
          base.ViewDidLoad();
          // Perform any additional setup after loading the view, typically from a nib.

          TranslateButton.TouchUpInside += (object sender, EventArgs e) => {
            // Convert the phone number with text to a number
            // using PhoneTranslator.cs
            translatedNumber = PhoneTranslator.ToNumber(
              PhoneNumberText.Text);

            // Dismiss the keyboard if text field was tapped
            PhoneNumberText.ResignFirstResponder();

            if (translatedNumber == "")
            {
              CallButton.SetTitle("Call ", UIControlState.Normal);
              CallButton.Enabled = false;
            }
            else
            {
              CallButton.SetTitle("Call " + translatedNumber,
                UIControlState.Normal);
              CallButton.Enabled = true;
            }
          };

          CallButton.TouchUpInside += (object sender, EventArgs e) => {

            //Store the phone number that we're dialing in PhoneNumbers
            PhoneNumbers.Add(translatedNumber);

            // Use URL handler with tel: prefix to invoke Apple's Phone app...
            var url = new NSUrl("tel:" + translatedNumber);

            // otherwise show an alert dialog
            if (!UIApplication.SharedApplication.OpenUrl(url))
            {
              var alert = UIAlertController.Create("Not supported", "Scheme 'tel:' is not supported on this device", UIAlertControllerStyle.Alert);
              alert.AddAction(UIAlertAction.Create("Ok", UIAlertActionStyle.Default, null));
              PresentViewController(alert, true, null);
            }
          };
        }

        public override void PrepareForSegue(UIStoryboardSegue segue, NSObject sender)
        {
          base.PrepareForSegue(segue, sender);

          // set the View Controller that’s powering the screen we’re
          // transitioning to

          var callHistoryContoller = segue.DestinationViewController as CallHistoryController;

          //set the Table View Controller’s list of phone numbers to the
          // list of dialed phone numbers

          if (callHistoryContoller != null)
          {
            callHistoryContoller.PhoneNumbers = PhoneNumbers;
          }
        }
      }
    }
    ```


Здесь необходимо обратить внимание на несколько моментов.
  * Переменная `translatedNumber` перемещена из метода `ViewDidLoad` в _переменную уровня класса_.
  * Код **CallButton** изменен, чтобы добавлять набранные номера в список телефонных номеров с помощью вызова `PhoneNumbers.Add(translatedNumber)`.
  * Добавлен метод `PrepareForSegue`.

  Сохраните изменения и выполните сборку приложения, чтобы убедиться в отсутствии ошибок.

20. Нажмите кнопку **Запустить**, чтобы запустить приложение в **симуляторе iOS**:

  ![](hello-ios-multiscreen-quickstart-images/19.png "Нажмите кнопку \"Запустить\", чтобы запустить приложение в симуляторе iOS")


Поздравляем! Вы создали свое первое приложение Xamarin.iOS с несколькими экранами!

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

## <a name="walkthrough"></a>Пошаговое руководство

В этом пошаговом руководстве вы добавите в приложение **Phoneword** экран "Call History" (Журнал вызовов).


1. Откройте приложение **Phoneword** в Visual Studio. При необходимости скачайте [готовое приложение Phoneword](https://developer.xamarin.com/samples/monotouch/Hello_iOS/) из пошагового руководства [Привет, iOS](~/ios/get-started/hello-ios/index.md). Не забывайте, что для подключения к [Mac](~/ios/get-started/installation/windows/connecting-to-mac/index.md) нужно использовать конструктор iOS и симулятор iOS.


2. Сначала измените пользовательский интерфейс. Откройте файл **Main.storyboard** в **обозревателе решений** и убедитесь, что в поле **Просмотреть как** задано значение _iPhone 6_:

  ![](hello-ios-multiscreen-quickstart-images/image1.png "Файл Main.storyboard в конструкторе iOS")


3. Перетащите **контроллер навигации** из **панели элементов** в область конструктора:

  ![](hello-ios-multiscreen-quickstart-images/image2.png "Перетаскивание контроллера навигации из панели элементов в область конструктора")


4. Перетащите **переход без источника** (это серая стрелка слева от сцены **Phoneword**) из сцены **Phoneword** на **контроллер навигации**, чтобы изменить начальную точку приложения:

  ![](hello-ios-multiscreen-quickstart-images/image3.png "Перетаскивание перехода без источника на контроллер навигации для изменения начальной точки приложения")


5. Выберите **контроллер корневого представления**, щелкнув черную полосу, а затем нажмите клавишу **DELETE**, чтобы удалить его из области конструктора.
  Переместите сцену **Phoneword** к **контроллеру навигации**:

  ![](hello-ios-multiscreen-quickstart-images/image4.png "Перемещение сцены Phoneword к контроллеру навигации")


6. Задайте **ViewController** в качестве `Root View Controller` контроллера навигации. Нажмите и удерживайте клавишу **CTRL** и щелкните внутри **контроллера навигации**. Должна появиться синяя линия. Затем, продолжая удерживать клавишу **CTRL**, перетащите элементы из **контроллера навигации** в сцену **Phoneword**. Это называется _перетаскиванием с удержанием клавиши CTRL_:

  ![](hello-ios-multiscreen-quickstart-images/image5.png "Перетаскивание элементов из контроллера навигации в сцену Phoneword")


7. В контекстном меню задайте связь **Корень**:

  ![](hello-ios-multiscreen-quickstart-images/image6.png "Задание связи \"Корень\"")

  Теперь **ViewController** является **контроллером корневого представления у контроллера навигации**.


8. Дважды щелкните **Phoneword** экрана **заголовок** панели и изменить **заголовок** для **Phoneword**:

  ![](hello-ios-multiscreen-quickstart-images/image7.png "Изменение заголовка на Phoneword")


9. Перетащите элемент **Button** из **панели элементов** и поместите его под элементом **Call Button** (Кнопка вызова). Перетащите маркеры, чтобы сделать новый элемент **Button** такой же ширины, что и элемент **Call Button** (Кнопка вызова):

  ![](hello-ios-multiscreen-quickstart-images/image8.png "Сделайте новый элемент \"Button\" такой же ширины, что и элемент \"Call Button\" (Кнопка вызова)")


10. В **обозревателе свойств** измените **Имя** с **Button** на `CallHistoryButton` и измените **Заголовок** на **Call History** (Журнал вызовов):

  ![](hello-ios-multiscreen-quickstart-images/image9.png "Измените \"Имя\" с \"Button\" на \"CallHistoryButton\" и \"Заголовок\" на \"Call History\" (Журнал вызовов)")


11. Создайте экран **Call History** (Журнал вызовов). Перетащите **контроллер представления таблиц** из **панели элементов** в область конструктора:

  ![](hello-ios-multiscreen-quickstart-images/image10.png "Перетащите контроллер представления таблиц в область конструктора")


12. Выберите **контроллер представления таблиц**, щелкнув черную полосу в нижней части сцены. В **обозревателе свойств** измените класс **контроллера представления таблиц** на `CallHistoryController` и нажмите клавишу **ВВОД**:

  ![](hello-ios-multiscreen-quickstart-images/image11.png "Измените класс контроллеров представления таблицы на CallHistoryController")

  Конструктор IOS создает пользовательский резервный класс `CallHistoryController` для управления иерархией представлений содержимого на этом экране.
  В **обозревателе решений** появляется файл **CallHistoryController.cs**:

  ![](hello-ios-multiscreen-quickstart-images/image12.png "Файл CallHistoryController.cs в обозревателе решений")


13. Дважды щелкните файл **CallHistoryController.cs**, чтобы открыть его, и замените содержимое следующим кодом:

        using System;
        using Foundation;
        using UIKit;
        using System.Collections.Generic;

        namespace Phoneword
        {
            public partial class CallHistoryController : UITableViewController
            {
                public List<String> PhoneNumbers { get; set; }

                static NSString callHistoryCellId = new NSString ("CallHistoryCell");

                public CallHistoryController (IntPtr handle) : base (handle)
                {
                    TableView.RegisterClassForCellReuse (typeof(UITableViewCell), callHistoryCellId);
                    TableView.Source = new CallHistoryDataSource (this);
                    PhoneNumbers = new List<string> ();
                }

                class CallHistoryDataSource : UITableViewSource
                {
                    CallHistoryController controller;

                    public CallHistoryDataSource (CallHistoryController controller)
                    {
                        this.controller = controller;
                    }

                    // Returns the number of rows in each section of the table
                    public override nint RowsInSection (UITableView tableView, nint section)
                    {
                        return controller.PhoneNumbers.Count;
                    }

                    public override UITableViewCell GetCell (UITableView tableView, NSIndexPath indexPath)
                    {
                        var cell = tableView.DequeueReusableCell (CallHistoryController.callHistoryCellId);

                        int row = indexPath.Row;
                        cell.TextLabel.Text = controller.PhoneNumbers [row];
                        return cell;
                    }
                }
            }
        }

  Сохраните приложение и выполните его сборку, чтобы убедиться в отсутствии ошибок. На данном этапе можно игнорировать любые предупреждения сборки.


14. Создайте _переход_ между сценой **Phoneword** и сценой **Call History** (Журнал вызовов).
  В **сцене Phoneword** выберите **Call History Button** (Кнопка журнала вызовов) и, **удерживая нажатой клавишу CTRL, перетащите** из элемента **Button** в сцену **Call History** (Журнал вызовов):

  ![](hello-ios-multiscreen-quickstart-images/image13.png "Удерживая нажатой клавишу CTRL, перетащите из элемента \"Button\" в сцену \"Call History\" (Журнал вызовов)")

  В контекстном меню **Action Segue** (Переход между действиями) выберите **Показать**:

  ![](hello-ios-multiscreen-quickstart-images/image14.png "Выбор типа перехода \"Показать\"")

  Конструктор iOS добавляет переход между двумя сценами:

  ![](hello-ios-multiscreen-quickstart-images/image15.png "Переход между двумя сценами")


15. Добавьте **Заголовок** в **контроллер представления таблиц**, выбрав черную полосу в нижней части сцены и изменив **Контроллер представления > Заголовок** на **Call History** (Журнал вызовов) в **обозревателе свойств**:

  ![](hello-ios-multiscreen-quickstart-images/image16.png "Изменение значения \"Контроллер представления > Заголовок\" на \"Call History\" (Журнал вызовов)")


16. При запуске приложения **Call History Button** (Кнопка журнала вызовов) откроет экран **Call History** (Журнал вызовов), однако представление таблиц будет пустым, так как отсутствует код для отслеживания и отображения телефонных номеров.

  Это приложение сохраняет телефонные номера в виде списка строк.

  Добавьте директиву `using` для `System.Collections.Generic` в начало **ViewController**:

        using System.Collections.Generic;

17. Измените класс `ViewController` с помощью следующего кода:

    ```csharp
    using System;
    using System.Collections.Generic;
    using Foundation;
    using UIKit;

    namespace Phoneword_iOS
    {
      public partial class ViewController : UIViewController
      {
        string translatedNumber = "";

        public List<string> PhoneNumbers { get; set; }

        protected ViewController(IntPtr handle) : base(handle)
        {
          //initialize list of phone numbers called for Call History screen
          PhoneNumbers = new List<string>();
        }

        public override void ViewDidLoad()
        {
          base.ViewDidLoad();
          // Perform any additional setup after loading the view, typically from a nib.

          TranslateButton.TouchUpInside += (object sender, EventArgs e) => {
            // Convert the phone number with text to a number
            // using PhoneTranslator.cs
            translatedNumber = PhoneTranslator.ToNumber(
              PhoneNumberText.Text);

            // Dismiss the keyboard if text field was tapped
            PhoneNumberText.ResignFirstResponder();

            if (translatedNumber == "")
            {
              CallButton.SetTitle("Call ", UIControlState.Normal);
              CallButton.Enabled = false;
            }
            else
            {
              CallButton.SetTitle("Call " + translatedNumber,
                UIControlState.Normal);
              CallButton.Enabled = true;
            }
          };

          CallButton.TouchUpInside += (object sender, EventArgs e) => {

            //Store the phone number that we're dialing in PhoneNumbers
            PhoneNumbers.Add(translatedNumber);

            // Use URL handler with tel: prefix to invoke Apple's Phone app...
            var url = new NSUrl("tel:" + translatedNumber);

            // otherwise show an alert dialog
            if (!UIApplication.SharedApplication.OpenUrl(url))
            {
              var alert = UIAlertController.Create("Not supported", "Scheme 'tel:' is not supported on this device", UIAlertControllerStyle.Alert);
              alert.AddAction(UIAlertAction.Create("Ok", UIAlertActionStyle.Default, null));
              PresentViewController(alert, true, null);
            }
          };
        }

        public override void PrepareForSegue(UIStoryboardSegue segue, NSObject sender)
        {
          base.PrepareForSegue(segue, sender);

          // set the View Controller that’s powering the screen we’re
          // transitioning to

          var callHistoryContoller = segue.DestinationViewController as CallHistoryController;

          //set the Table View Controller’s list of phone numbers to the
          // list of dialed phone numbers

          if (callHistoryContoller != null)
          {
            callHistoryContoller.PhoneNumbers = PhoneNumbers;
          }
        }
      }
    }
    ```

Здесь необходимо обратить внимание на несколько моментов.
  * Переменная `translatedNumber` перемещена из метода `ViewDidLoad` в _переменную уровня класса_.
  * Код **CallButton** изменен, чтобы добавлять набранные номера в список телефонных номеров с помощью вызова `PhoneNumbers.Add(translatedNumber)`.
  * Добавлен метод `PrepareForSegue`.

  Сохраните изменения и выполните сборку приложения, чтобы убедиться в отсутствии ошибок.

  Сохраните изменения и выполните сборку приложения, чтобы убедиться в отсутствии ошибок.


20. Нажмите кнопку **Запустить**, чтобы запустить приложение в **симуляторе iOS**.

  ![](hello-ios-multiscreen-quickstart-images/19.png "Первый экран примера приложения")


Поздравляем! Вы создали свое первое приложение Xamarin.iOS с несколькими экранами!


-----

Теперь приложение может обрабатывать навигацию как с помощью переходов, так и в коде. Пришло время закрепить и углубить приобретенные знания и навыки — вас ждет раздел [Привет, iOS (несколько экранов). Подробные сведения](~/ios/get-started/hello-ios-multiscreen/hello-ios-multiscreen-deepdive.md).


## <a name="related-links"></a>Связанные ссылки

- [Привет, iOS (пример)](https://developer.xamarin.com/samples/monotouch/Hello_iOS/)
- [Рекомендации по работе с человеческим интерфейсом iOS](http://developer.apple.com/library/ios/#documentation/UserExperience/Conceptual/MobileHIG/Introduction/Introduction.html)
- [Портал подготовки iOS](https://developer.apple.com/ios/manage/overview/index.action)
