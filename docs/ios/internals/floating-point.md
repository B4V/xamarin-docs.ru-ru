---
title: Операций с плавающей точкой в Xamarin.iOS
description: В этом документе описываются как Xamarin.iOS обрабатывает 32-разрядных и 64-разрядных точность вычислений с плавающей запятой и связанные влияют на производительность.
ms.prod: xamarin
ms.assetid: 003F25C1-B430-4339-9C95-7DF527EBC699
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.openlocfilehash: c5ee1b833e309c78c7338298cbe5c8800afb1ba1
ms.sourcegitcommit: e268fd44422d0bbc7c944a678e2cc633a0493122
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50116242"
---
# <a name="floating-point-operations-in-xamarinios"></a>Операций с плавающей точкой в Xamarin.iOS

Xamarin.iOS будет по умолчанию выполнять 32-разрядных и 64-разрядные операции с плавающей запятой с помощью 64-битной точности на ARM.  

Хотя это более высокой точностью ближе к что ожидать разработчики от операций с плавающей точкой в C# на рабочем столе, на мобильных устройствах, может быть значительное влияние на производительность.

Существует возможность компиляции кода с плавающей точки 32-разрядных использовать 32-разрядные операции с плавающей запятой.  Чтобы сделать это, необходимо использовать по крайней мере Xamarin.iOS 8.10 и set в iOS построения панель параметров на «mtouch дополнительных аргументов» запись строки следующее значение:

     --aot-options=-O=float32

Этим действием вы сообщите компиляторы статических (встроенные статический компилятор Mono, или один на основе LLVM) для выполнения операции с плавающей запятой, используя 32-разрядных значения с плавающей запятой.
