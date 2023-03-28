## Схема устройства CVMFS

<img class="op-uc-image op-uc-image_inline" src="/api/v3/attachments/9/content">

Где:

Stratum0 - главный сервер CVMFS, на котором происходит создание и изменения в репозиториях

Stratum1 - сервера репликации, разворачиваемые в зонах тестирования, реплицирующих необходимые репозитории с Stratum0 и распространающие репозитории в своей зоне тестирования

proxy - сервера для распределения нагрузки между клиентами CVMFS

client - конечное устройсво, на которые монтируются репозитории CVMFS

## Развертывание CVMFS на Stratum0

Развертывание Stratum0 сервера выполняется на ОС debian11.

Сперва необходимо подключить репозитории cvmfs для debian и установить пакеты cvmfs и cvmfs-server

```bash
wget https://ecsft.cern.ch/dist/cvmfs/cvmfs-release/cvmfs-release-latest_all.deb
dpkg -i cvmfs-release-latest_all.deb
rm -f cvmfs-release-latest_all.deb
apt update
apt install cvmfs cvmfs-server
```

Репозитории создаются следующим образом

```bash
root@cvmfs:~# cvmfs_server mkfs distr.aq.ru
Owner of distr.aq.ru [root]: 
Creating Configuration Files... done
Creating CernVM-FS Master Key and Self-Signed Certificate... done
Creating CernVM-FS Server Infrastructure... done
Creating Backend Storage... done
Signing 30 day whitelist with master key... done
Creating Initial Repository... done
Mounting CernVM-FS Storage... (overlayfs) done
Allowing Replication of this Repository... done
Initial commit... New CernVM-FS repository for distr.aq.ru
Updating global JSON information... done

Before you can install anything, call `cvmfs_server transaction`
to enable write access on your repository. Then install your
software in /cvmfs/distr.aq.ru as user root.
Once you're happy, publish using `cvmfs_server publish`

For client configuration, have a look at 'cvmfs_server info'

If you go for production, backup your masterkey from /etc/cvmfs/keys/!
```

После создания репозитория, мы получим следующие сущности:

**/etc/cvmfs/keys** - содержаться ключи сгенерированные репозиторием для доступа и управления, все ключи созданного репозитория начинаются с названия репозитория.

**/cvmfs/distr.aq.ru** - директория для редактирование содержащихся в репозитории файлов, доступная только в момент, пока репозиторий не опубликован.

Для внесения изменений в репозиторий необходимо перевести репозиторий в статус transaction

```bash
root@cvmfs:~# cvmfs_server transaction distr.aq.ru 
```

Теперь по пути **/cvmfs/distr.aq.ru/** можно вносить изменения в репозиторий.
Сперва необходимо в новом репозитории создать файл .cvmfsdirtab с описание структуры папок репозитория. Пример:
```bash
/images/*
/isos/*
/packages/*
```
После внесения всех изменений в репозиторий, его нужно опубликовать (предварительно нужно выйти из репозитория, или будет показанно сообщения что опубликовать репозиторий невозможно)
```bash
root@cvmfs:/cvmfs/distr.aq.ru# cvmfs_server publish distr.aq.ru distr.aq.ru 
Current working directory is in /cvmfs/distr.aq.ru.  Please release, e.g. by 'cd $HOME'.
root@cvmfs:/cvmfs/distr.aq.ru# cd ..
root@cvmfs:/cvmfs# cvmfs_server publish distr.aq.ru distr.aq.ru 
Using auto tag 'generic-2022-10-07T16:33:08Z'
Processing changes...
...................................
Waiting for upload of files before committing...
Committing file catalogs...
Wait for all uploads to finish
Exporting repository manifest
Statistics stored at: /var/spool/cvmfs/distr.aq.ru/stats.db
Tagging distr.aq.ru
Flushing file system buffers
Signing new manifest
Remounting newly created repository revision
```
Посмотреть информацию о созданном репозитории, и получить инсрукцию для подключения клиента к репозиторию можно следующим образом
```bash
root@cvmfs:/cvmfs# cvmfs_server info distr.aq.ru 
Repository name: distr.aq.ru
Created by CernVM-FS 143
Stratum1 replication allowed: yes
Whitelist is valid for another 29 days

Client configuration:
Add distr.aq.ru to CVMFS_REPOSITORIES in /etc/cvmfs/default.local
Create /etc/cvmfs/config.d/distr.aq.ru.conf and set
  CVMFS_SERVER_URL=http://localhost/cvmfs/distr.aq.ru
  CVMFS_PUBLIC_KEY=/etc/cvmfs/keys/distr.aq.ru.pub
Copy /etc/cvmfs/keys/distr.aq.ru.pub to the client
```