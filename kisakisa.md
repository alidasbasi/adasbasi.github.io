---
layout: page
title: Karalama Defterim
subtitle: 
---

# Ubuntu

```bash
$ lsb_release -a # checking ubuntu version
```

# Postgresql

## Kurulum

```sh
$ sudo apt-get update
$ sudo apt-get install postgresql postgresql-contrib
```

## Roller

- Roller Unix/Linux sistem hesaplarıyla benzer.
- Postgres rol adı, Unix/Linux sistem hesabı ile aynı.
- default rol/kullanıcı: postgres


```bash
# Rol oluşturma
$ sudo -u postgres createuser --interactive # komut sonrası prompt gelecek
$ sudo adduser yeni_kullanici_adi

# Rol/kullanıcı değiştirme
$ sudo -i -u postgres
$ psql

veya

$ sudo -u postgres psql

# Tanımlı rol/kullanıcı
postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------
 ali       | Superuser, Create role, Create DB                          | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```

## Veritabanı Oluşturma

- Öntanımlı olarak rol ismi ile veritabı ismide aynı.
- yeni rol oluştururken veritabanıda oluşturuluyor.


```bash
$ sudo -u postgres createdb yeni_kullanici_adi

# Veritabanlarını listele

postgres=# \l
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges   
-----------+----------+----------+-------------+-------------+-----------------------
 ali       | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
(4 rows)
```

## Yeni rol ile oturum açma

```bash
$ sudo -i -u kullanici_adi
$ psql
# \conninfo

# Output
You are connected to database "kullanici_adi" as user "kullanici_adi" via socket in "/var/run/postgresql" at port "5432".

# \c postgres 
You are connected to database "postgres" as user "kullanici_adi" via socket in "/var/run/postgresql" at port "5432".
```

## Tablo Oluşturma

```bash

ali=# create table deneme (
id serial PRIMARY KEY,
baslik varchar (50) NOT NULL
    );
CREATE TABLE

ali=# \dt
        List of relations
 Schema |  Name  | Type  | Owner 
--------+--------+-------+-------
 public | deneme | table | ali
(1 row)

```


