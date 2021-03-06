# Билет №5
## СКВ. Основные функции и термины, базовые принципы

__Системы контроля версий__ — это программные системы, хранящие несколько версий одного документа, и позволяющие вернуться к более ранним версиям. Как правило, для каждого изменения запоминается дата модификации и автор.

## Функции

* История изменений
    * Откат дефектных изменений
    * Извлечение кода "из прошлого"
    * Поиск ошибок сравнением
* Централизованное хранение
    * Актуальное и используемое всеми участниками
    * Защищенное, с разграничением прав доступа

## Термины

* __Рабочая директория__ (Working Directory)
    * Рабочая директория – это место, где файлы проверяются. Git не отслеживает каждый изменённый файл
    * Когда мы выполняем операцию commit, Git ищет все файлы, которые находятся в рабочей директории
    * Подтверждаются только те файлы, которые в ней находятся
* __Локальный репозиторий__ (Local Repository)
    * Личное рабочее пространство для работы с проектом
    * Разработчик вносит изменения в проект в этом репозитории и, после подтверждения изменений, они становятся частью локальной копии
    * Пользователь может выполнить множество изменений, которые будут храниться только на его машине до тех пор, пока он не отправит их в центральный репозиторий
* __Дерево__ (Tree)
    * Объект, который представляет собой директорию
    * Хранит бинарные большие объекты как под-директории
    * Дерево – это бинарный файл, который хранит ссылки на, так называемые, Blobs и деревья, которые представлены SHA1 хэшем объекта дерева.
* __Бинарный Большой Объект__  (Blob или Binary Large Object)
    * Файл, который представляет версию файла
    * Содержит данные файла, но не хранит его метаданные
    * Это двоичный объект и в базе данных Git он называется SHA1 хэшем файла
    * В Git доступ к файлам обеспечивается не по имени, а по содержанию.
* __Коммит__ (Commit)
    * Хранит текущее состояние репозитория 
    * Также называется SHA1 хэшем
    * Можно представить, что commit – это элемент связного списка
        * Каждый такой элемент имеет ссылку на родительский элемент
        * Из этого элемента мы можем откатиться назад с помощью ссылки на предыдущий элемент для того
    * Если у коммита есть несколько родительских коммитов, то это означает, что он был создан путём слияния двух ветвей
* __Клон__ (Clone)
    * Экземпляр репозитория
    * Не только проверяет рабочую копию, но также становится хранилищем самого репозитория (зеркалом – mirror)
    * Разработчик может выполнять множество операций на локальной машине, а после подключения к сети все данные могут быть синхронизированы
* __Ветвь__ (Branch)
    * Ветви используются для создания отдельной версии разработки
    * По умолчанию, Git имеет главную ветвь, которая называется master
    * При необходимости реализовать какой-либо функционал, или исправить ошибку, создаётся отдельная ветвь и выполняется необходимую работу
    * После того как задача выполнена, выполняется слияние с веткой master/development и ненужная ветвь удаляется
    * Это позволяет всегда хранить рабочую версию проекта и вносить уже полностью готовые и протестированные изменения в основную ветвь
* __Pull__ (Вытягивать)
    * Копирование всех изменений из удалённого репозитория на локальную машину
    * Используется для синхронизации локального репозитория с центральным
* __Push__ (Толчок)
    * Копирует изменения из локального репозитория в удалённый
    * Используется для синхронизации центрального репозитория с локальным
* __Заголовок__ (HEAD)
    * Ссылка, которая всегда указывает на крайний коммит ветви
    *  Когда мы выполняем операцию commit, HEAD обновляется и переводится на крайний коммит

## Базовые принципы

* Каждому проекту следует выработать свой рабочий процесс и правила именования веток. При этом желательно основываться на популярных подходах
* Приложение строится только на на основе известного состояния репозитория
    * Не только релизы, но и экспериментальные и тестовые сборки (builds)
    * В идеале приложение умеет сообщать свою ревизию и параметры сборки
* Стабильность общих (публичных) веток
    * Они обязаны компилироваться и проходить все тесты в любой момент времени
    * Изменения тестируются до попадания в репозиторий
    * Если дефектные изменения прошли, они исправляются в срочном порядке
* Абсолютно вся разработка фиксируется в истории
    * Это делается в виде отдельных веток локального или глобального репозитория
    * "Удачные" изменения добавляются в основную ветвь
* Публичная история проекта не "переписывается"
    * Однажды помеченные тэгами и выпущенные релизы модификации не подлежат
    * Промежуточная история не переписывается, потому что будут конфликты

## Понятие API, совместимости на уровне исходных кодов и бинарной, критерии и рекомендации

__API__ (Application Programming Interface) — набор готовых классов, процедур, функций, структур и констант, предоставляемых ОС, приложением, библиотекой для использования во внешних программных продуктах.

__Совместимость на уровне API__ — совместимость на уровне исходного кода на языке программирования. Замена библиотеки на другую не ломает компиляцию и логику программы.

__ABI__ (Application Binary Inerface) — бинарный интерфейс программ и библиотек, включающий в себя соглашения о вызовах, передаче параметров, обработке исключений и других сущностей языков программирования.

__Бинарная совместимость__ — совместимость на уровне скомпилированных модулей. Модуль можно заменить другим без потерь.

* Все современные ОС предоставляют API
* Все прикладные приложения явно или косвенно от него зависят
* Необходимо поддерживать совместимость

### Способы реализации API & ABI

* Программные прерывания процессора
* Динамическая компоновка и вызов библиотечных функции
* Формирование пакетов данных соответствующих общим соглашениям, протоколы
