🛠 При сборке образа Docker ищет файл с исключениями, исходя из имени основного файла конфигурации. Например, команда `docker build -f myapp.Dockerfile .` будет в первую очередь искать файл исключений по пути `myapp.Dockerfile.dockerignore`. Если такого файла не найдётся, то при наличии будет использоваться `.dockerignore`.

🛠  Все объекты Docker обязательно имеют имя. Если оно не назначается пользователем, то в качестве имени используется хэш. Чтобы работать с образами было удобнее, лучше выбирать имя. Кроме имени можно также использовать тэги. Обычно тэги указывают на версию или особенности той или иной сборки образа. Совокупность образов с одним именем, но разными тэгами, — это репозиторий образов. Например, можно собрать образ с указанием имени и тэга командой:

```bash
docker build -t vieux/apache:2.0 .
```

Имя образа `vieux/apache` использует принятое в терминологии Docker соглашение. До слэша `/` указывается имя пользователя, после — имя образа или репозитория образов. В качестве имени пользователя чаще всего подразумевается имя пользователя в реестре репозиториев. Исторически первым и самым крупным является официальный реестр компании Docker — [Docker Hub](https://hub.docker.com).

После двоеточия `:` можно указать тэг. В примере этот тэг обозначает версию сборки, но тэги также могут указывать и на вариант образа, например, на основе Alpine Linux или Ubuntu. Вы можете указать с помощью тэга, что версия базового образа должна быть последней, и в момент сборки именно она попадёт в образ.

🛠  Важно отслеживать размер образа, и пользоваться образами с умом. Вы можете загрузить к себе образ командой `pull`. Например, для образа Node.js:

```bash
docker pull node
```

Уже на этапе клонирования образа вы увидите его размер. После скачивания и установки  также можно получить информацию об образе с помощью команды:

```bash
docker image inspect node
```

В терминале будет выведена информация об образе в формате JSON. По ключу `"Size"` можно увидеть размер образа в байтах. Большое внимание в технологии Docker уделяется скорости сборки и размеру образов. Именно поэтому рекомендуется использовать наименьший образ операционной системы, который обеспечивает весь набор инструментов и служб, необходимый для запускаемого приложения. Практически стандартом стало использование Alpine Linux в качестве базовой операционной системы. В официальном репозитории образов Node.js есть образ и на основе этой операционной системы: `node:lts-alpine`.
