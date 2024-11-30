# Домашнее задание к занятию «Компоненты Kubernetes»- Михалёв Сергей

### Цель задания

Рассчитать требования к кластеру под проект

------

### Задание. Необходимо определить требуемые ресурсы
Известно, что проекту нужны база данных, система кеширования, а само приложение состоит из бекенда и фронтенда. Опишите, какие ресурсы нужны, если известно:

1. Необходимо упаковать приложение в чарт для деплоя в разные окружения. 
2. База данных должна быть отказоустойчивой. Потребляет 4 ГБ ОЗУ в работе, 1 ядро. 3 копии. 
3. Кеш должен быть отказоустойчивый. Потребляет 4 ГБ ОЗУ в работе, 1 ядро. 3 копии. 
4. Фронтенд обрабатывает внешние запросы быстро, отдавая статику. Потребляет не более 50 МБ ОЗУ на каждый экземпляр, 0.2 ядра. 5 копий. 
5. Бекенд потребляет 600 МБ ОЗУ и по 1 ядру на копию. 10 копий.

----

**Решение**

Необходимые ресурсы по компонентам

**База данных** (отказоустойчивая)

Тип: StatefulSet (для сохранения состояния и отказоустойчивости).

- Ресурсы:
** Память: 4 ГБ на под.
  **CPU: 1 ядро на под.
- Количество копий: 3.
    Хранилище: Персистентное (PersistentVolume) для каждого пода.
    Примерное хранилище: 20–50 ГБ на каждую реплику (зависит от нагрузки и данных).
    Сетевые ресурсы: Headless Service для доступа к каждому поду по имени.
