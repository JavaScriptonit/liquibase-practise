# liquibase-practise
```
git add .
git commit -m "add Liquibase ansible files for postgres"
git push -u origin main
```
---
### 1. Установка и настройка Liquibase
1. **Установили Java**:
   - Liquibase требует Java для работы, поэтому мы установили OpenJDK 11.

2. **Скачали и установили Liquibase**:
   - Скачали архив с Liquibase, распаковали его и установили в `/usr/local/bin`.

3. **Создали структуру проекта**:
   - Создали директорию `/opt/liquibase-project/changelogs` для хранения файлов изменений (changelogs).

4. **Скопировали конфигурационные файлы**:
   - Скопировали файл `liquibase.properties`, который содержит настройки подключения к PostgreSQL.
   - Скопировали файлы changelog (`db.changelog-master.xml`, `001-create-users-table.xml`, `002-create-orders-table.xml`), которые описывают изменения в базе данных.

5. **Применили изменения в базе данных**:
   - Запустили команду `liquibase update`, которая применила изменения, описанные в changelog-файлах, к базе данных.

---

### 2. Liquibase — это утилита командной строки

Liquibase — это утилита командной строки, которая выполняет задачи и завершает свою работу. Она не запускается как сервис или демон, поэтому вы не увидите её в списке процессов после завершения выполнения.

Когда вы запускаете команду `liquibase update`, она:
1. Подключается к базе данных.
2. Проверяет, какие изменения нужно применить.
3. Применяет изменения.
4. Завершает работу.

---

### 3. Документация к плейбуку `update_liquibase.yml`

#### Описание плейбука
Плейбук `update_liquibase.yml` выполняет следующие задачи:

1. **Устанавливает Java**:
   - Устанавливает OpenJDK 11, необходимый для работы Liquibase.

2. **Скачивает и устанавливает Liquibase**:
   - Скачивает архив с Liquibase и распаковывает его в `/usr/local/bin`.

3. **Создаёт структуру проекта**:
   - Создаёт директорию `/opt/liquibase-project/changelogs` для хранения файлов изменений.

4. **Копирует конфигурационные файлы**:
   - Копирует файл `liquibase.properties`, который содержит настройки подключения к PostgreSQL.
   - Копирует файлы changelog (`db.changelog-master.xml`, `001-create-users-table.xml`, `002-create-orders-table.xml`), которые описывают изменения в базе данных.

5. **Применяет изменения в базе данных**:
   - Запускает команду `liquibase update`, которая применяет изменения, описанные в changelog-файлах, к базе данных.

#### Переменные
- `db_name`: Имя базы данных.
- `db_user`: Имя пользователя базы данных.
- `db_password`: Пароль пользователя базы данных.
- `postgres_password`: Пароль для пользователя `postgres`.

#### Файлы
- `files/liquibase.properties.j2`: Шаблон конфигурации Liquibase.
- `files/db.changelog-master.xml`: Главный файл changelog, который включает другие файлы изменений.
- `files/001-create-users-table.xml`: Файл изменений для создания таблицы `users`.
- `files/002-create-orders-table.xml`: Файл изменений для создания таблицы `orders`.

---

### 4. Что можно сделать с помощью Liquibase?

Liquibase — это мощный инструмент для управления изменениями в базе данных. Вот что ещё можно делать с его помощью:

#### Основные команды
1. **Применение изменений (`update`)**:
   - Применяет изменения из changelog-файлов к базе данных.
   ```bash
   liquibase update
   ```

2. **Откат изменений (`rollback`)**:
   - Откатывает изменения до определённой точки (например, до тега или количества изменений).
   ```bash
   liquibase rollback <tag>
   ```

3. **Проверка состояния базы данных (`status`)**:
   - Показывает, какие изменения ещё не применены.
   ```bash
   liquibase status
   ```

4. **Генерация SQL-скрипта (`updateSQL`)**:
   - Генерирует SQL-скрипт для применения изменений, но не выполняет его.
   ```bash
   liquibase updateSQL
   ```

5. **Создание отчёта (`generate-changelog`)**:
   - Генерирует changelog-файл на основе существующей базы данных.
   ```bash
   liquibase generate-changelog
   ```

#### Примеры использования
1. **Создание таблиц**:
   - Вы можете создавать таблицы, добавлять столбцы, индексы и ограничения.

2. **Изменение структуры базы данных**:
   - Добавлять или удалять столбцы, изменять типы данных, добавлять внешние ключи.

3. **Миграции между окружениями**:
   - Применять одинаковые изменения в разных окружениях (dev, staging, production).

4. **Версионирование базы данных**:
   - Отслеживать изменения в базе данных с помощью changelog-файлов.

5. **Интеграция с CI/CD**:
   - Автоматически применять изменения при деплое приложения.

#### Пример changelog для добавления столбца
```xml
<changeSet id="3" author="devops">
    <addColumn tableName="users">
        <column name="phone" type="varchar(20)"/>
    </addColumn>
</changeSet>
```

#### Пример changelog для удаления таблицы
```xml
<changeSet id="4" author="devops">
    <dropTable tableName="orders"/>
</changeSet>
```

---

### Итог
- **Liquibase** — это инструмент для управления изменениями в базе данных.
- Он не запускается как сервис, а выполняет команды и завершает работу.
- С помощью Liquibase можно создавать таблицы, изменять структуру базы данных, выполнять миграции и многое другое.
