---
title: Создание службы Android
description: В этом руководстве рассматриваются службы Xamarin.Android, которые являются компоненты Android, позволяющие должны быть выполнены без active пользовательский интерфейс. Службы очень часто используются для задач, выполняемых в фоновом режиме, такие как много времени вычислений, загрузка файлов, воспроизведение музыки и т. д. Он объясняет различные сценарии, подходящие для служб и показано, как реализовать их как для выполнения длительных фоновых задач, а также для предоставления интерфейса для удаленных вызовов процедур.
ms.prod: xamarin
ms.assetid: BA371A59-6F7A-F62A-02FC-28253504ACC9
ms.technology: xamarin-android
author: conceptdev
ms.author: crdun
ms.date: 03/19/2018
ms.openlocfilehash: b9aa29507ebb37e3912b1027419e47c82832dfa9
ms.sourcegitcommit: e268fd44422d0bbc7c944a678e2cc633a0493122
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50116515"
---
# <a name="creating-android-services"></a>Создание службы Android

_В этом руководстве рассматриваются службы Xamarin.Android, которые являются компоненты Android, позволяющие должны быть выполнены без active пользовательский интерфейс. Службы очень часто используются для задач, выполняемых в фоновом режиме, такие как много времени вычислений, загрузка файлов, воспроизведение музыки и т. д. Он объясняет различные сценарии, подходящие для служб и показано, как реализовать их как для выполнения длительных фоновых задач, а также для предоставления интерфейса для удаленных вызовов процедур._

## <a name="android-services-overview"></a>Обзор служб Android

Мобильные приложения ничем не напоминают Классические приложения. Рабочие столы имеют большое количество ресурсов, таких как площадь экрана, память, дисковое пространство и подключенных источников питания, мобильных устройств — нет. Эти ограничения принудительно мобильные приложения, вести себя по-разному. Например небольшом экране на мобильном устройстве обычно означает, что одновременно отображается, только одно приложение (т. е. действие). Другие действия перемещен в фоновом режиме и передаче в приостановленном состоянии, где они не могут выполнять какой-либо работы. Тем не менее только потому, что приложение Android находится в фоновом режиме означает, что его невозможно для приложения продолжить работу. 

Приложения Android, состоящего из по крайней мере один из следующих четырех основных компонентов: _действия_, _широковещательных получателей_, _поставщики содержимого_и _Служб_. Действия являются краеугольным камнем много отличных приложений Android, так как они предоставляют пользовательский Интерфейс, который позволяет пользователю взаимодействовать с приложением. Тем не менее когда дело доходит до выполнения параллельной или фоновой работы, действий не всегда лучший выбор.
 
Является основным механизмом для фоновой работы в Android _службы_. Службу Android — это компонент, который позволяет выполнить некоторую работу без пользовательского интерфейса. Услуга может загрузить файл, воспроизведение музыки или применить фильтр к изображению. Службы могут также использоваться для взаимодействия между процессами (_IPC_) между приложений Android. Например, одно приложение Android может использовать служба проигрывателя музыки, из другого приложения или приложение может предоставлять данные (например, контактные данные человека) в другие приложения с помощью службы. 

Службы и возможности для выполнения фоновой работы, имеют решающее значение для предоставления интерфейса smooth и гибких пользовательских. Все приложения Android имеют _основной поток_ (также известный как _поток пользовательского интерфейса_), на котором выполняются действия. Чтобы обеспечить быстрые устройства, Android необходимо иметь возможность обновить пользовательский интерфейс со скоростью 60 кадров в секунду. Если приложение Android выполняет слишком много работы в основном потоке, а затем Android приведет к удалению кадров, что в свою очередь вызывает пользовательский Интерфейс отображается рывками (иногда также называют _janky_). Это означает, что вся работа, произведенная в потоке пользовательского интерфейса должно завершиться в промежутке времени между двумя фреймами примерно 16 миллисекунд (1 второй каждые 60 кадров). 

Чтобы устранить эту проблему, разработчик может использовать потоки в действии для выполнения определенных действий, блокировка пользовательского интерфейса. Тем не менее это может вызвать проблемы. Это очень возможно, что Android уничтожит и повторно создать несколько экземпляров действия. Тем не менее Android, не будут нарушены автоматически потоков, что может привести к утечке памяти. Хорошим примером этого является, если [повороте устройства](~/android/app-fundamentals/handling-rotation.md) &ndash; Android будет пытаться уничтожить экземпляр действия, а затем повторно создайте его:

![При повороте устройства, 1 уничтожается и создается экземпляр 2](images/image-01.png)

Это происходит утечка памяти &ndash; по-прежнему выполняется поток, созданный в первом экземпляре действия. Если поток имеет ссылку на первый экземпляр действия, это будет препятствовать Android сборки мусора, сбором объекта. Однако второй экземпляр действия по-прежнему создается (который в свою очередь может создать новый поток). Поворот устройства несколько раз подряд может исчерпать весь объем ОЗУ и принудительно Android для завершения работы всего приложения, чтобы освободить память.

Как правило если работа, которую можно выполнить должна пережить действия, затем службы должны создаваться для выполнения этой работы. Тем не менее если работа применим только в контексте действия, затем создание потока для выполнения работы может быть более подходящим. Например Создание эскиза для фотографии, который был только что добавлен к коллекции фотоприложению должно выполняться, скорее всего, в службе. Однако поток может быть более подходящим решением может воспроизводить музыкальные, который должен быть слышен только во время действия находится на переднем плане.

Фоновую работу можно разделить на две широкие категории:

1. **Long запуск задачи** &ndash; это работы, которая будет завершена, пока не будет остановлен явным образом. Пример _долго выполняющиеся задачи_ — приложение, которое выполняет потоковую передачу музыки или, необходимо отслеживать данные, собранные с датчика. Эти задачи необходимо запустить, несмотря на то, что приложение не имеет видимого пользовательского интерфейса.
2. **Периодические задачи** &ndash; (иногда называется _задания_) периодическую задачу — это приложения, имеет относительно короткий в длительность (несколько секунд) и выполняется по расписанию (т. е. один раз в день, неделю или, возможно, только один раз в Далее 60 секунд). Примером этого загрузки файла из Интернета или создание эскиз для изображения.

Существует четыре различных типа службы Android:

* **Привязки службы** &ndash; объект _привязан службы_ — это служба, с какой-либо компонент (обычно действие) привязанным к нему. Связанные службы предоставляет интерфейс, позволяющий связанный компонент и службе взаимодействовать друг с другом. Как только будут Дополнительные клиенты не привязан к службе, Android завершит работу службы. 

* **`IntentService`** &ndash; _`IntentService`_ Является специализированным подклассом `Service` класс, который упрощает создание службы и использования. `IntentService` Предназначен для обработки отдельных вызовов автономной. В отличие от службы, который может одновременно обрабатывать несколько вызовов, `IntentService` , больше напоминает _работы очереди процессора_ &ndash; рабочих помещается в очередь и `IntentService` обрабатывает каждое задание одной за раз в одном рабочем потоке. Как правило`IntentService` не привязан к действию или фрагментом. 

* **Служба запущена** &ndash; объект _запустил службу_ — это служба, который был запущен по какой-либо Android компонент (например, действие) и выполняется непрерывное в фоновом режиме, пока что-то явно сообщает остановки службы. В отличие от привязки службы службы не имеет любых клиентов, напрямую привязанными к нему. По этой причине важно разработать запущенные службы, таким образом, чтобы они могут быть корректно перезагружены при необходимости.

* **Гибридная служба** &ndash; объект _гибридная служба_ — это служба, которая имеет характеристики _запустил службу_ и _привязан службы_. Гибридная служба можно запустить, когда компонент привязывает к нему, или оно может начаться либо событием. Клиентский компонент может или не может быть привязан к службе гибридной. Гибридная служба продолжит работу до ее явным образом сообщать, чтобы остановить или существуют дополнительные клиенты не привязанным к нему.

Какой тип службы, используемой в значительной степени зависят от требований приложения. Как правило `IntentService` или привязанной службы достаточно для большинства задач, которые должно выполнять приложение на платформе Android, поэтому предпочтение следует уделить один из этих двух типов служб. `IntentService` Хорошо подходит для задач «одноступенчатая», например загрузку файла, хотя привязанную службу подойдет при необходимости частого взаимодействия с действие/фрагмент. 

Хотя большинство служб выполняется в фоновом режиме, есть специальные подкатегорию, известный как _службы переднего плана_. Это служба, которому предоставлен более высокий приоритет (по сравнению с обычной службе) для выполнения определенных действий для пользователя (например, воспроизведение музыки). 

Также возможен запуск службы в собственный процесс на одном устройстве, это иногда называется _удаленной службы_ или как _вне процесса службы_. Для этого требуются дополнительные усилия, чтобы создать, но может быть полезно для когда приложению требуется совместного использования функциональных возможностей с другими приложениями и в некоторых случаях усовершенствовать взаимодействие с пользователем приложения. 

### <a name="background-execution-limits-in-android-80"></a>Ограничения выполнения фона в Android 8.0

Начиная с Android 8.0 (уровень API 26), приложение Android больше не иметь возможность свободно выполнения в фоновом режиме. Когда он находится на переднем плане, приложение можно запустить и выполнить служб без ограничений. Когда приложение перемещает в фоновом режиме, Android предоставляет приложение некоторое время на запуск и использование служб. После истечения этого времени, приложение больше не могут запускать все службы, и все службы, которые были запущены будет прервано. Эта точка находится AT не поддерживается на какой-либо работы приложения. Android считает, что приложение может на переднем плане, если выполнено одно из следующих условий:

* Есть отображается действие (запущена или приостановлена).
* Приложение запущено службы переднего плана.
* Другое приложение находится на переднем плане и используются компоненты из приложения, которое бы в противном случае в фоновом режиме. Примером этого является, если приложение A, которая находится на переднем плане, привязан к службу, предоставляемую приложения б. приложение Б также будут считаться на переднем плане и не завершен системой Android за активное участие в фоновом режиме.

Существуют ситуации, когда, несмотря на то, что приложение — в фоновом режиме, Android будет пробуждения приложения и смягчать эти ограничения в течение нескольких минут, что позволяет приложению для выполнения определенных действий:
* Высокий приоритет Firebase Cloud сообщения, полученные приложением.
* Приложение получает вещания. 
* Приложение получает выполняет `PendingIntent` в ответ на уведомление.

Существующие приложения Xamarin.Android может потребоваться изменить, как они выполняют фоновой работы, чтобы избежать проблем, которые могут возникнуть в Android 8.0. Ниже приведены некоторые практические alterantives в службу Android.

* **Запланируйте работу для запуска в фоновом режиме, используя планировщик заданий Android или [диспетчер заданий Firebase](~/android/platform/firebase-job-dispatcher.md)**  &ndash; эти две библиотеки предоставляют платформу для приложений на разделении фоновая работа в _заданий_, дискретные единицу работы. Приложения можно затем запланировать задания в операционную систему, а также некоторые критерии о, когда задание может выполняться.
* **Запустите службу на переднем плане** &ndash; службы переднего плана подходит, когда приложение должно выполнить некоторую задачу в фоновом режиме, и ему может потребоваться периодически взаимодействовать с этой задачей. Службы переднего плана будет отображаться постоянного уведомления, чтобы пользователю сообщается, что приложение выполняется в фоновом режиме и также предоставляет способ отслеживания или взаимодействовать с этой задачей. Примером этого бы в приложении возможности создания подкастов, воспроизведение подкаст пользователю или возможно загрузка эпизод подкаст, чтобы позже можно удовольствие. 
* **Использовать высокий приоритет сообщения Firebase Cloud (FCM)** &ndash; при Android получает высокий приоритет FCM для приложения, она позволит это приложение для запуска служб в фоновом режиме на короткое время. Это может быть хорошей альтернативой необходимости фоновая служба, которая опрашивает приложения в фоновом режиме. 
* **Отложить действий по обеспечению момент приложения на передний план** &ndash; Если ни одно из предыдущих решений являются приемлемыми, то приложения необходимо разработать собственные способы для приостановки и возобновления работы, когда приложение отображается на переднем плане.

## <a name="related-links"></a>Связанные ссылки

* [Ограничивает Android Oreo фонового выполнения](https://www.youtube.com/watch?v=Pumf_4yjTMc)
