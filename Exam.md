# Что такое docker, rkt, containerd? Как работает контейнеризация в одной из выбранных систем на выбор? 

## Что такое docker, rkt, containerd

Docker — это платформа контейнеризации с открытым исходным кодом, с помощью которой можно автоматизировать создание приложений, их доставку и управление. Платформа позволяет быстрее тестировать и выкладывать приложения, запускать на одной машине требуемое количество контейнеров.

Rocket (rkt) является альтернативой Docker, разработанной для серверной среды с наиболее строгими требованиями к безопасности и производительности. rkt ориентирован на спецификацию App Container, набор простых и открытых инструкций для формата портативных контейнеров.

Containerd — это управляющая программа для управления жизненным циклом контейнера — от скачивания и распаковки образа контейнера до выполнения контейнера и контроля его работы.

## Docker

Docker состоит из трех проектов:

1. docker-cli: утилита командной строки, с которой вы взаимодействуете с помощью команды docker.

2. containerd: Linux Daemon, который управляет контейнерами и запускает их. Он загружает образы из репозитория, управляет хранилищем и сетью, а также контролирует работу контейнеров.

3. runc: низкоуровневая среда выполнения контейнеров, которая создает и запускает контейнеры.

## Основные понятия Docker

Образы (Images)

Docker-образ — это read-only шаблон. Например, образ может содержать ОС Ubuntu c Apache и приложением на ней. Образы используются для создания контейнеров. Docker позволяет легко создавать новые образы, обновлять существующие, или вы можете скачать образы созданные другими людьми. Образы — это компонента сборки docker-а.

Реестр (Registry)

Docker-реестр хранит образы. Есть публичные и приватные реестры, из которых можно скачать либо загрузить образы. Публичный Docker-реестр — это Docker Hub. Там хранится огромная коллекция образов. 

Контейнеры (Containers)

Контейнеры похожи на директории. В контейнерах содержится все, что нужно для работы приложения. Каждый контейнер создается из образа. Контейнеры могут быть созданы, запущены, остановлены, перенесены или удалены. Каждый контейнер изолирован и является безопасной платформой для приложения. Контейнеры — это компонента работы.

## Используемые технологии в Docker

1. Namespaces

Docker использует технологию namespaces для организации изолированных рабочих пространств, которые мы называем контейнерами. Когда мы запускаем контейнер, docker создает набор пространств имен для данного контейнера.

Это создает изолированный уровень, каждый аспект контейнера запущен в своем простанстве имен, и не имеет доступ к внешней системе.

Список некоторых пространств имен, которые использует docker:
* pid: для изоляции процесса;
* net: для управления сетевыми интерфейсами;
* ipc: для управления IPC ресурсами. (ICP: InterProccess Communication);
* mnt: для управления точками монтирования;
* utc: для изолирования ядра и контроля генерации версий(UTC: Unix timesharing system).

2. Control groups

Docker также использует технологию cgroups или контрольные группы. Ключ к работе приложения в изоляции, предоставление приложению только тех ресурсов, которые вы хотите предоставить. Это гарантирует, что контейнеры будут хорошими соседями. Контрольные группы позволяют разделять доступные ресурсы железа и если необходимо, устанавливать пределы и ограничения. Например, ограничить возможное количество памяти контейнеру.

3. Union File System

Union File Sysem или UnionFS — это файловая система, которая работает создавая уровни, делая ее очень легковесной и быстрой. Docker использует UnionFS для создания блоков, из которых строится контейнер. Docker может использовать несколько вариантов UnionFS включая: AUFS, btrfs, vfs и DeviceMapper.

## Виды сетей в docker

В докере 6 типов сетей(сетевых драйверов):

1. Bridge: в этой сети контейнеры запускаются по умолчанию. Связь устанавливается через bridge-интерфейс на хосте. У контейнеров, которые используют одинаковую сеть, есть своя собственная подсеть, и они могут передавать данные друг другу по умолчанию.

2. Host: этот драйвер дает контейнеру доступ к собственному пространству хоста (контейнер будет видеть и использовать тот же интерфейс, что и хост).

3. Macvlan: этот драйвер дает контейнерам прямой доступ к интерфейсу и суб-интерфейсу (vlan) хоста. Также он разрешает транкинг.

4. Overlay: этот драйвер позволяет строить сети на нескольких хостах с Docker (обычно на Docker Swarm кластере). У контейнеров также есть свои адреса сети и подсети, и они могут напрямую обмениваться данными, даже если они располагаются физически на разных хостах.

5. Null: тип сети при котором контейнер создается без IP адреса, т.е. изолированно. нельзя создать несколько сетей типа Null на одном хосте.


# Понятие хардфорка, его причины и последствия. Примеры хардфорков в различных сетях.

## Основные положения

1. Хардфорк — метод внесения существенных изменений в код протокола блокчейн-проекта.

2. Хардфорк является своеобразным способом достичь консенсус относительно новых изменений в комьюнити.

3. Иногда хардфорки используют для запуска новых криптопроектов.

## Что такое форк

Форк — это создание копии программного обеспечения и его модификация. При этом первоначальный проект продолжает функционировать, но форк развивается отдельно в своем направлении. Предположим, что внутри команды некого сайта с криптовалютой возникли серьезные разногласия по поводу дальнейшего развития. Тогда одна часть команды может воссоздать сайт в другом домене, где они будут размещать другой контент.

Оба этих проекта построены на одной основе и имеют общую историю подобно тому, как одна дорога разделяется на два разных направления.

## Зачем нужен хардфорк

Каждый блокчейн работает на базе какого-то протокола — приложения, состоящего из различных компонентов. Код протокола большинства популярных блокчейн-проектов открыт. Это значит, что он опубликован целиком и его можно свободно копировать.

Код блокчейн-протоколов постоянно дорабатывают: убирают найденные ошибки и уязвимости и добавляют улучшения. Некоторые из этих изменений могут быть довольно масштабными. Тогда разработчики и производят хардфорк: не меняют текущую версию протокола, а создают параллельную его копию, куда добавляют новый код. А уже затем валидаторы или операторы биткоин-нод переходят на новую версию протокола. Конечно, если они согласны с предложенными изменениями.

Таким образом, Хардфорки — это обновление программного обеспечения, несовместимое с предыдущими версиями. Это происходит, когда ноды добавляют изменения, противоречащие существующим правилам старых нод. Новые ноды могут взаимодействовать только с нодами, использующими новую версию. В результате блокчейн разделяется на две отдельные сети: одну со старыми правилами и другую — с новыми.

## Чем софтфорк отличается от хардфорка

Если хардфорк — это «жесткое» обновление, которое требует перехода на новую «ветку», то софтфорк — «мягкие», обычно несущественные изменения, для которых не нужно перезапускать сеть на новом протоколе.

## Примеры хардфорков

### Хардфорк Биткоина в 2017 году 

В качестве примера хардфорка можно привести форк 2017 года, в результате которого Биткоин был разделен на два чейна — оригинальный Биткоин (BTC) и новый Bitcoin Cash (BCH). Форк появился в результате долгих споров о наилучшем подходе к масштабированию. Сторонники Bitcoin Cash хотели увеличить размер блока, а сторонники Биткоина выступили против этого изменения.

### Xардфорк London в блокчейне Ethereum

Хардфорк Ethereum под названием London – это обновление, которое затрагивает модель комиссий за транзакции в блокчейне и «бомбу сложности». После обновления в сети Ethereum аукцион ставок на газ была заменена на базовую комиссию за каждый блок.

Хардфорк представит два новых предложения по улучшению сети Ethereum (EIP). Обновление London предназначалось для подготавки почвы для перехода платформы на алгоритм Proof of Stake. В связи с подготовкой к версии Serenity майнерам придется столкнуться с замедлением работы и повышением сложности майнинга. 

Главное изменение заключается в новом механизме дефляции комиссий за транзакции. Ранее пользователи оплачивали газ в формате аукциона, и майнеры отдавали предпочтение транзакциям с наибольшей комиссией, поскольку комиссия превращалась в вознаграждение за добавленный блок. После обновления каждый блок будет иметь фиксированную комиссию.