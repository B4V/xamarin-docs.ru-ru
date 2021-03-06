---
title: Ход выполнения и индикаторы активности в Xamarin.iOS
description: В этом документе описывается использование индикаторы хода выполнения и действия в Xamarin.iOS. В этом примере описывает использование их программно или с помощью раскадровки.
ms.prod: xamarin
ms.assetid: 7AA887E4-51F7-4867-82C5-A8D2EA48AE07
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 07/11/2017
ms.openlocfilehash: cb56af300444020a543c16afb0dfb48015fc2153
ms.sourcegitcommit: e268fd44422d0bbc7c944a678e2cc633a0493122
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50102598"
---
# <a name="progress-and-activity-indicators-in-xamarinios"></a>Ход выполнения и индикаторы активности в Xamarin.iOS

Вполне вероятно, что приложения должны выполнять длительно выполняемые задачи, например загрузки или обработки данных и что эта задержка может привести к задержке при обновлении пользовательского интерфейса. В это время следует всегда использовать индикатор хода выполнения, чтобы уверить пользователя, что система занята работой. Это предоставляет пользовательский элемент управления, приложение работает на свой запрос, который не ожидает входные данные, и может обеспечивать содержит подробные сведения о точности, как долго они придется ждать.

iOS предоставляет два основных способа для предоставления этот индикатор хода выполнения в приложении: индикаторы активности (включая конкретного _сети_ индикатор активности) и индикаторы выполнения.

## <a name="activity-indicator"></a>Индикатор активности

Индикаторы активности должен отображаться, когда ваше приложение работает много времени, но вы не знаете точный продолжительность времени, требует выполнения задачи.

Apple имеет следующие рекомендации по работе с индикаторы активности:

- **По возможности следует использовать вместо полосы хода выполнения** — так как индикатор активности предоставляет пользователю ни один отзыв о том, как долго выполняемый процесс займет, всегда используйте индикатор хода выполнения, если длина является знаете (например, сколько байтов для загрузки в файле).
- **Сохранить анимированный индикатор** -пользователи связаны стационарные индикатор активности остановленная приложение, должны всегда иметь индикатор, анимировать, хотя он отображается.
- **Описания задачи обработки** -простого отображения индикатора активности сама по себе недостаточно, пользователь должен быть в курсе процесса, они ожидают. Включить значимые метку (обычно один, полное предложение), очевидно, определяющий задачу.

### <a name="implementing-an-activity-indicator"></a>Реализация индикатор активности

Индикатор активности реализуется с помощью [ `UIActivityIndictorView` ](https://developer.xamarin.com/api/type/UIKit.UIActivityIndicatorView/) класс, чтобы указать, что `UIActivity` выполняется.

### <a name="activity-indicators-and-storyboards"></a>Индикаторы активности и раскадровки

При использовании конструктора iOS для создания пользовательского интерфейса, индикатор активности можно добавить в макет из области элементов. Из панели свойств можно изменить следующие свойства:

![Панель свойств](progress-activity-indicator-images/progress-indicator1.png)

### <a name="managing-activity-indicator-behavior"></a>Управление поведением индикатор активности

Используйте `StartAnimating()` и `StopAnimating()` методы для запуска и остановки анимации индикатор активности.

Задайте `HidesWhenStopped` свойства `true` вносить исчезают после индикатора активности `StopAnimating()` был вызван. Это имеет значение `true` по умолчанию. В любой момент можно увидеть, если индикатор активности выполняется путем проверки его анимации вращающейся `IsAnimating` свойство. 


### <a name="managing-activity-indicator-appearances"></a>Управление внешний вид индикатора активности

`UIActivityIndicatorViewStyle` Перечисления можно передать как параметр при создании экземпляра индикатора активности. Это можно использовать для задания визуальный стиль `Gray`, `White`, или `WhiteLarge`, например:

```csharp
activitySpinner = new UIActivityIndicatorView(UIActivityIndicatorViewStyle.WhiteLarge);
```

Вы можете переопределить цвет, предоставляемые `UIActivityIndicatorViewStyle` , задав `Color` свойство.

## <a name="progress-bar"></a>Progress Bar

Индикатор хода выполнения представляется в виде линий, заполняется цветом, чтобы указать состояние и длину трудоемкой задачей. Всегда следует использовать индикаторы выполнения, при длину задачах будет знать или может быть вычислено.

Apple имеет следующие рекомендации по работе с индикаторы выполнения.

- **Точно сообщать о ходе выполнения** -индикаторы выполнения всегда должно быть точное представление время, необходимое для выполнения задачи. Никогда не исказить того, чтобы сделать приложение прерываться.
- **Используйте для длительности Well-Defined** -индикатор хода выполнения должна отображаться не только что провайдер занимает размещения, но дает пользователя и указывает, какая часть задачи завершения, а также оценку оставшегося времени.

### <a name="implementing-an-progress-bar"></a>Реализация индикатор хода выполнения

Индикатор хода выполнения создается путем создания экземпляра [`UIProgressView`](https://developer.xamarin.com/api/type/UIKit.UIProgressView/)

### <a name="progress-bars-and-storyboards"></a>Индикаторы выполнения и раскадровки

Можно также добавить индикатор хода выполнения для пользовательского интерфейса при использовании конструктора iOS. Поиск **представление хода выполнения** в **элементов** и перетащите его в представление.

На панели свойств можно изменить следующие свойства:

![Панель свойств](progress-activity-indicator-images/progress-indicator3.png)


### <a name="managing-progress-bar-behavior"></a>Управление поведением индикатор хода выполнения

Ход выполнения панели изначально задаются с помощью `Progress` свойство:

```csharp
ProgressBar.Progress = 0f;
```

Ход выполнения можно изменить с помощью `SetProgress` передачей логическое значение, объявления, если необходимо, чтобы изменение анимации или нет.

```csharp
ProgressBar.SetProgress(1.0f, true);
```

Дополнительные сведения об использовании индикатора выполнения, см. [отчетов о ходе выполнения](https://github.com/xamarin/recipes/tree/master/Recipes/cross-platform/networking/download_progress) рецепт и [UICatalog tvOS пример](https://developer.xamarin.com/samples/monotouch/tvos/UICatalog/).

### <a name="managing-progress-bar-appearance"></a>Управление внешний вид индикатора хода выполнения

Аналогичную индикатор активности `UIProgressViewStyle` перечисления можно передать как параметр при создании экземпляра индикатор хода выполнения.

Ход выполнения и отслеживания образа и оттенок цвета можно изменить с помощью следующих свойств:

```csharp
progressBar = new UIProgressView(UIProgressViewStyle.Default)
            {
                ProgressImage = UIImage.FromBundle("TrackImage"),
                ProgressTintColor = UIColor.Cyan,
                TrackImage = UIImage.FromBundle("TrackImage"),
                TrackTintColor = UIColor.Magenta
            }; 
```



