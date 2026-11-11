# Домашнее задание к занятию 11 «Teamcity»

## Выполненные шаги

1. **Инстансы в Yandex Cloud**:
   - TeamCity Server (4 vCPU, 4 GB RAM), образ `jetbrains/teamcity-server`.
   - TeamCity Agent (2 vCPU, 4 GB RAM), образ `jetbrains/teamcity-agent`.
   - Nexus VM (2 vCPU, 4 GB RAM), установлен через Ansible playbook.

2. **TeamCity**:
   - Агент авторизован.
   - Проект создан на основе форка `example-teamcity`.
   - Условия сборки: `mvn clean test` для всех веток, кроме `master`; `mvn clean deploy` для `master`.
   - Загружен `settings.xml` с кредами для Nexus.
   - Настроены `Artifact Paths`: `**/target/*.jar => *.jar`.
   - Конфигурация мигрирована в Kotlin DSL.

3. **Nexus**:
   - Создан hosted-репозиторий `maven-releases` с политикой `Allow redeploy`.
   - В `pom.xml` добавлена секция `distributionManagement` с URL Nexus.

4. **Ветки**:
   - В `feature/add_reply` добавлен метод `reply()` со словом `hunter` и тест.
   - Сборка ветки прошла успешно (`mvn clean test`).
   - Ветка слита в `master`, выполнен деплой в Nexus.

5. **Артефакты**:
   - В Nexus в `maven-releases` появился `.jar` (`plaindoll-0.0.2.jar`).
   - В TeamCity на вкладке **Artifacts** сборки по `master` доступен `.jar`.

## Ссылки

- Форк `example-teamcity`: https://github.com/akamsoft/example-teamcity