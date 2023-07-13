# Data storage and resources.

## Deployment

### Deploy the PV.
```bash
kubectl apply -f pv.yaml
```

### Deploy the PVC.
```bash
kubectl apply -f pvc.yaml
```

### The environment variables are need by the cluster.
```bash
kubectl apply -f secret.yaml
kubectl apply -f configmap.yaml
```

### Create the deployment and add pod replica.
```bash
kubectl apply -f deployment.yaml
```

### Run the service to expose the cluster.
```bash
kubectl apply -f service.yaml
```

## Result of checking.

![alt text](https://github.com/anton-png/conteinerization/blob/main/assets/IMG_02.png?raw=true)

### Connect.
```bash
kubectl exec -it [pod-name]  --  psql -h localhost -U testuser --password -p 5432 testdatabase
```



## Домашнее задание к уроку 4 - Хранение данных и ресурсы
Напишите deployment для запуска сервера базы данных Postgresql.

Приложение должно запускаться из образа postgres:10.13

Должен быть описан порт:

5432 TCP
В деплойменте должна быть одна реплика, при этом при обновлении образа НЕ ДОЛЖНО одновременно работать несколько реплик. (то есть сначала должна удаляться старая реплика и только после этого подниматься новая).

Это можно сделать или с помощью maxSurge/maxUnavailable или указав стратегию деплоя Recreate.

В базе данных при запуске должен автоматически создаваться пользователь testuser с паролем testpassword. А также база testdatabase.

Для этого нужно указать переменные окружения POSTGRES_PASSWORD, POSTGRES_USER, POSTGRES_DB в деплойменте. При этом значение переменной POSTGRES_PASSWORD должно браться из секрета.

Так же нужно указать переменную PGDATA со значением /var/lib/postgresql/data/pgdata См. документацию к образу https://hub.docker.com/_/postgres раздел PGDATA

База данных должна хранить данные в PVC c размером диска в 10Gi, замонтированном в pod по пути /var/lib/postgresql/data

Проверка
Для проверки работоспособности базы данных:

Узнайте IP пода postgresql
kubectl get pod -o wide

Запустите рядом тестовый под
kubectl run -t -i --rm --image postgres:10.13 test bash

Внутри тестового пода выполните команду для подключения к БД
psql -h <postgresql pod IP из п.1> -U testuser testdatabase

Введите пароль - testpassword

Все в том же тестовом поде, после подключения к инстансу БД выполните команду для создания таблицы
CREATE TABLE testtable (testcolumn VARCHAR (50) );

Проверьте что таблица создалась. Для этого все в том же тестовом поде выполните команду
\dt

Выйдите из тестового пода. Попробуйте удалить под с postgresql.

После его пересоздания повторите все с п.1, кроме п.4 Проверьте что созданная ранее таблица никуда не делась.