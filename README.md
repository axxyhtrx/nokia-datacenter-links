# nokia-datacenter-links
Набор ссылок по теме Nokia Datacenter


# Nokia DC Stack — ресурсы

Ссылки для тех, кто только начинает разбираться с SR Linux и Nokia DC-стеком. 

---

## Containerlab

Утилита для поднятия сетевых топологий в контейнерах. Сделана Nokia-инженерами, полностью в открытом доступе.

- [containerlab.dev](https://containerlab.dev/) — сайт
- [Quick Start](https://containerlab.dev/quickstart/) — установка и первая топология с SR Linux + cEOS за 5 минут
- [Установка](https://containerlab.dev/install/) — deb/rpm, curl-скрипт, есть поддержка macOS и WSL
- [Supported Kinds](https://containerlab.dev/manual/kinds/) — что вообще можно запускать (SR Linux, SR OS, Arista cEOS, Cisco XRd и др.)
- [Topology Definition](https://containerlab.dev/manual/topo-def-file/) — синтаксис clab-файла
- [Lab Catalog](https://containerlab.dev/lab-examples/lab-examples/) — примеры топологий, идут вместе с пакетом

Если нет под рукой Linux-машины:
- [Codespaces](https://containerlab.dev/manual/codespaces/) — запуск в облаке бесплатно, прямо в браузере
- [clabernetes](https://containerlab.dev/manual/clabernetes/) — если хочется гонять топологии поверх k8s(например в облаке или если нужно запустить много)

GitHub:
- [srl-labs/containerlab](https://github.com/srl-labs/containerlab)
- [srl-labs/learn-srlinux](https://github.com/srl-labs/learn-srlinux)

---

## SR Linux

NOS на базе Linux, gNMI-first, с поддержкой кастомных агентов. Приложения портированы с SR OS. Образ публичный, без регистрации и лицензий.

### Документация

- [documentation.nokia.com/srlinux](https://documentation.nokia.com/srlinux/) — официальная дока, с выбором версии
- `doc.srlinux.dev/25-10` — короткий URL для конкретной версии, удобно в закладки
- [Release Notes](https://doc.srlinux.dev/rn25-10-1) — что появилось в последнем релизе

### Обучение

- [learn.srlinux.dev](https://learn.srlinux.dev/) — основной учебный ресурс, там туториалы, концепции и лабы
- [Get Started](https://learn.srlinux.dev/get-started/) — начать отсюда: образ, CLI, первые gNMI-запросы
- [Блог](https://learn.srlinux.dev/blog/) — статьи от команды Nokia DevRel, там много практики
- [YouTube Nokia](https://www.youtube.com/@nokianetworks) — видео по SR Linux

### Управление и автоматизация

- [JSON-RPC Basics](https://learn.srlinux.dev/tutorials/programmability/json-rpc/basics/) — как работает JSON-RPC интерфейс, примеры через curl
- [Ansible + SR Linux](https://learn.srlinux.dev/tutorials/programmability/ansible/using-nokia-srlinux-collection/) — nokia.srlinux collection, gNMI vs JSON-RPC
- [gnmic](https://gnmic.openconfig.net/) — CLI-клиент для gNMI на Go, очень удобен в работе
- [srlinux-yang-models](https://github.com/nokia/srlinux-yang-models) — все YANG-модели
- [yang.srlinux.dev](https://yang.srlinux.dev/) — браузер YANG-моделей онлайн

### DC Fabric / EVPN

- [L2 EVPN туториал](https://learn.srlinux.dev/tutorials/l2evpn/intro/) — EVPN-VXLAN L2: underlay + overlay + сервис, пошагово
- [L2 EVPN: eBGP underlay](https://learn.srlinux.dev/tutorials/l2evpn/fabric/) — конфигурация underlay с нуля
- [L3 EVPN RT5-only](https://learn.srlinux.dev/tutorials/l3evpn/rt5-only/) — L3 EVPN с BGP Unnumbered (с версии 24.3.1)
- [L3 EVPN: BGP PE-CE](https://learn.srlinux.dev/tutorials/l3evpn/rt5-only/l3evpn-bgp-pe-ce/) — CE с eBGP в ip-vrf
- [SR Linux + Kubernetes + MetalLB](https://learn.srlinux.dev/blog/2023/exposing-kubernetes-services-to-sr-linux-based-ip-fabric-with-anycast-gateway-and-metallb/) — как подружить IP-фабрику с k8s через anycast GW

### NDK

- [ndk-greeter-go](https://github.com/srl-labs/ndk-greeter-go) — hello-world NDK агент на Go, отправная точка если хочется писать свои агенты

---

## EDA (Event Driven Automation)

Платформа для автоматизации DC-фабрики. Работает поверх Kubernetes, управляет SR Linux через gNMI. Модель декларативная — описываешь что хочешь, EDA разбирается как это сделать на железе. Есть транзакционная модель с откатом, git как база данных состояния.

### C чего начать

- [docs.eda.dev](https://docs.eda.dev/25.12/) — документация (редирект с корня на актуальную версию)
- [Try EDA](https://docs.eda.dev/25.12/getting-started/try-eda/) — `make try-eda` и через ~10 минут готовый Playground с Digital Twin из трёх SR Linux нод
- [Tour of EDA](https://docs.eda.dev/25.12/tour-of-eda/) — последовательный разбор концепций с упражнениями
- [EDA в Codespaces](https://docs.eda.dev/25.12/software-install/non-production/codespaces/) — если хочется попробовать в браузере с установкой в 1 клик.

### Архитектура

- [Introducing EDA](https://documentation.nokia.com/eda/24-12/books/user/introduction.html) — официальный обзор: ConfigEngine, транзакции, git-as-database
- [Nodes](https://docs.eda.dev/25.12/tour-of-eda/nodes/) — как EDA работает с нодами, Digital Twin, deviation management
- [The beginning of an era](https://docs.eda.dev/blog/the-beginning-of-an-era-eda/) — стартовый пост с NFD demo, хорошо объясняет мотивацию создания продукта и его отличие от других систем
- [Nokia.com — EDA](https://www.nokia.com/data-center-networks/data-center-fabric/event-driven-automation/) — маркетинговый обзор, но с полезной структурой

### Разработка приложений под EDA

приложения в EDA это CRD и операторы, если разработчики умеют писать CRD под Kubernetes - они могут писать приложения для EDA.

- [REST API](https://docs.eda.dev/25.4/development/api/) — OpenAPI, Core API + Apps API
- [App Quick Start](https://docs.eda.dev/25.4/development/apps/quick-start/) — пишем кастомное приложение на MicroPython с edabuilder
- [nokia-eda (GitHub)](https://github.com/nokia-eda) — исходники, примеры, CRD

---

## Дополнительно

- [openconfig/public](https://github.com/openconfig/public) — OpenConfig YANG-модели, часть из них SR Linux поддерживает
- [openconfig/gnmi](https://github.com/openconfig/gnmi) — спецификация gNMI
- [awesome-network-automation](https://github.com/networktocode/awesome-network-automation) — большая коллекция инструментов для сетевой автоматизации
- [Discord](https://go.srlinux.dev/discord) — сообщество SR Linux / Containerlab / EDA, живые ответы на вопросы

---

Начать проще всего с [learn.srlinux.dev/get-started](https://learn.srlinux.dev/get-started/) — learning by doing,.
Если нет Linux под рукой, [Codespaces](https://containerlab.dev/manual/codespaces/) решает вопрос.
Ресурсы у бесплатной версии codespaces ограничены, заранее лучше посмотреть хватит ли вам времени для экспериментов. 
