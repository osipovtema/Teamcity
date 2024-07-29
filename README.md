# Домашнее задание к занятию 11 «Teamcity» - `Мурчин Артем`

## Подготовка к выполнению

1. В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`.
2. Дождитесь запуска teamcity, выполните первоначальную настройку.
3. Создайте ещё один инстанс (2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему переменную окружения `SERVER_URL: "http://<teamcity_url>:8111"`.
4. Авторизуйте агент.
5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity).
6. Создайте VM (2CPU4RAM) и запустите [playbook](./infrastructure).

## Решение - подготовка к выполнению

Создал три ВМ в соответствии с заданием:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-01-hw.png)

Авторизовал агент:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-02-hw.png)

Запустил [playbook](./infrastructure).

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-04-hw.png)

## Основная часть

1. Создайте новый проект в teamcity на основе fork.
2. Сделайте autodetect конфигурации.
3. Сохраните необходимые шаги, запустите первую сборку master.
4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`.
5. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.
6. В pom.xml необходимо поменять ссылки на репозиторий и nexus.
7. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.
8. Мигрируйте `build configuration` в репозиторий.
9. Создайте отдельную ветку `feature/add_reply` в репозитории.
10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`.
11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.
12. Сделайте push всех изменений в новую ветку репозитория.
13. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.
14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.
15. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.
16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.
17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.
18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.
19. В ответе пришлите ссылку на репозиторий.

## Решение - основная часть

1. Создал новый проект в teamcity на основе fork.
2. Сделал autodetect конфигурации.
3. Сохранил необходимые шаги, запустил первую сборку master. Сборка прошла успешно:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-05-hw.png)

4. Поменял условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-06-hw.png)

5. Для deploy загрузил [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-07-hw.png)

6. В pom.xml поменял ссылки на репозиторий и nexus:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-08-hw.png)

7. Запустил сборку по master, убедился, что всё прошло успешно и артефакт появился в nexus:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-09-hw.png)

8. Мигрировал `build configuration` в репозиторий:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-095-hw.png)

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-096-hw.png)

9. Создал отдельную ветку `feature/add_reply` в репозитории.
10. Написал новый метод для класса Welcomer: метод возвращает произвольную реплику, содержащую слово `hunter`:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-10-hw.png)

11. Дополнил тест для нового метода на поиск слова `hunter` в новой реплике:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-11-hw.png)

12. Сделал push всех изменений в новую ветку репозитория.
13. Убедился, что сборка самостоятельно запустилась, тесты прошли успешно:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-12-hw.png)

14. Сделал `Merge` ветки `feature/add_reply` в `master`.

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-13-hw.png)

15. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.
16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.
17. Провел повторную сборку мастера, но к сожалению сборка не прошла успешно и артефакты не собраны. Пробовал изменить версию в `pom.xml` на 0.0.2, но это не помогло. Все равно сборка не прошла:

![alt text](https://github.com/artmur1/19-05-teamcity-hw/blob/main/img/19-05-01-14-hw.png)

19. В ответе пришлите ссылку на репозиторий.

https://github.com/artmur1/example-teamcity

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---
