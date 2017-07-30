+++
title = "Belajar MySql/MariaDb"
date = "2017-07-06T21:49:20+02:00"
tags = ["mysql", "mariaDB"]
categories = ["database"]
author = "tipobrata"
+++

### Login ke terminal mysql

```
cd /opt/lampp/bin 

$ ./mysql -u testuser -p

```

### Create Table MASTER

```
create table t_master as
select 1 id, 'A' data union all
select 2 id, 'B' data union all
select 3 id, 'C' data;
```

```
MariaDB [testdb]> select * from t_master;
+----+------+
| id | data |
+----+------+
|  1 | A    |
|  2 | B    |
|  3 | C    |
+----+------+
3 rows in set (0.00 sec)

```

### Create Table TRANSAKSI 1

```
create table t_transaksi_1 as
select 1 id, 'DOC 1' doc, 2000 value union all
select 1 id, 'DOC 1' doc, 1000 value union all
select 2 id, 'DOC 2' doc, 5000 value union all
select 3 id, 'DOC 3' doc, 3000 value union all
select 3 id, 'DOC 4' doc, 3000 value union all
select 3 id, 'DOC 4' doc, 2000 value;
```

```
MariaDB [testdb]> select * from t_transaksi_1;
+----+-------+-------+
| id | doc   | value |
+----+-------+-------+
|  1 | DOC 1 |  2000 |
|  1 | DOC 1 |  1000 |
|  2 | DOC 2 |  5000 |
|  3 | DOC 3 |  3000 |
|  3 | DOC 4 |  3000 |
|  3 | DOC 4 |  2000 |
+----+-------+-------+
6 rows in set (0.00 sec)

```

### Create Table TRANSAKSI 2

```
create table t_transaksi_2 as
select 2 id, 'DOC 2' doc, 2000 value union all
select 2 id, 'DOC 2' doc, 2000 value union all
select 3 id, 'DOC 3' doc, 4000 value union all
select 3 id, 'DOC 4' doc, 5000 value union all
select 3 id, 'DOC 4' doc, 1000 value;
```

```
MariaDB [testdb]> select * from t_transaksi_2;
+----+-------+-------+
| id | doc   | value |
+----+-------+-------+
|  2 | DOC 2 |  2000 |
|  2 | DOC 2 |  2000 |
|  3 | DOC 3 |  4000 |
|  3 | DOC 4 |  5000 |
|  3 | DOC 4 |  1000 |
+----+-------+-------+
5 rows in set (0.00 sec)

```

### Menggunakan Group By

Sekarang kita buatkan summary untuk table TRANSAKSI pertama, menggunakan `GROUP BY` dan fungsi aggregat `SUM()`, menambahkan `value/nilai` dari `Doc` yang sama dan juga menampilkan `id` doc dari tabel master.

Contoh Penggunaannya:

```
SELECT tbl_names.id, tbl_section.id, name, section
  FROM tbl_names
  JOIN tbl_section ON tbl_section.id = tbl_names.id 

//Jika menggunakan alias
SELECT n.id, s.id, n.name, s.section
  FROM tbl_names n
  JOIN tbl_section s ON s.id = n.id 

```

Implementasi: 

```
select a.id, a.data, t.doc, sum(value) value1
from t_master a
join t_transaksi_1 t on t.id=a.id
group by id, doc;
```

Tampilan pada command: 

```
MariaDB [testdb]> select a.id, a.data, t.doc, sum(value) value1
    -> from t_master a
    -> join t_transaksi_1 t on t.id=a.id
    -> group by id, doc;
+----+------+-------+--------+
| id | data | doc   | value1 |
+----+------+-------+--------+
|  1 | A    | DOC 1 |   3000 |
|  2 | B    | DOC 2 |   5000 |
|  3 | C    | DOC 3 |   3000 |
|  3 | C    | DOC 4 |   5000 |
+----+------+-------+--------+
4 rows in set (0.00 sec)
```

### Menggunakan Group By dan Sum

Sekarang kita buatkan summary untuk table TRANSAKSI kedua, menggunakan GROUP BY dan fungsi aggregat SUM().

```
select a.id, a.data, tt.doc, sum(value) value2
from t_master a
join t_transaksi_2 tt on tt.id=a.id
group by id, doc;
```
Implementasi :

```
MariaDB [testdb]> select a.id, a.data, tt.doc, sum(value) value2
    -> from t_master a
    -> join t_transaksi_2 tt on tt.id=a.id
    -> group by id, doc;
+----+------+-------+--------+
| id | data | doc   | value2 |
+----+------+-------+--------+
|  2 | B    | DOC 2 |   4000 |
|  3 | C    | DOC 3 |   4000 |
|  3 | C    | DOC 4 |   6000 |
+----+------+-------+--------+
3 rows in set (0.00 sec)

```

### Menggunakan Left Join

Sekarang menggabungkan SUMMARY dari TRANSAKSI pertama dan kedua, menggunakan LEFT JOIN menjadi seperti ini.

command yang di gunakan: 

```
select res1.id, res1.data, res1.doc
, value1
, value2
from (
select tm.id, data, doc, sum(value) value1
from t_master tm
join t_transaksi_1 tr on tm.id=tr.id
group by id, doc
) res1
left join (
select tm.id, data, doc, sum(value) value2
from t_master tm
join t_transaksi_2 tr on tm.id=tr.id
group by id, doc
) res2 on res1.id=res2.id and res1.doc=res2.doc;
```

Implementasi:

```
MariaDB [testdb]> select res1.id, res1.data, res1.doc
    -> , value1
    -> , value2
    -> from (
    -> select tm.id, data, doc, sum(value) value1
    -> from t_master tm
    -> join t_transaksi_1 tr on tm.id=tr.id
    -> group by id, doc
    -> ) res1
    -> left join (
    -> select tm.id, data, doc, sum(value) value2
    -> from t_master tm
    -> join t_transaksi_2 tr on tm.id=tr.id
    -> group by id, doc
    -> ) res2 on res1.id=res2.id and res1.doc=res2.doc;
+----+------+-------+--------+--------+
| id | data | doc   | value1 | value2 |
+----+------+-------+--------+--------+
|  1 | A    | DOC 1 |   3000 |   NULL |
|  2 | B    | DOC 2 |   5000 |   4000 |
|  3 | C    | DOC 3 |   3000 |   4000 |
|  3 | C    | DOC 4 |   5000 |   6000 |
+----+------+-------+--------+--------+
4 rows in set (0.00 sec)

```
### Menggunakan Ifnull

Namun masih ada yang sedikit aneh, karena ada nilai NULL di sana, maka kita gunakan perintah IFNULL() untuk mengunbahknya menjadi angka 0 (nol).

```
select res1.id, res1.data, res1.doc
, ifnull(value1,0) value1
, ifnull(value2,0) value2
from (
select tm.id, data, doc, sum(value) value1
from t_master tm
join t_transaksi_1 tr on tm.id=tr.id
group by id, doc
) res1
left join (
select tm.id, data, doc, sum(value) value2
from t_master tm
join t_transaksi_2 tr on tm.id=tr.id
group by id, doc
) res2 on res1.id=res2.id and res1.doc=res2.doc;

```
Berikut Tampilan hasilnya:
```
MariaDB [testdb]> select res1.id, res1.data, res1.doc
    -> , ifnull(value1,0) value1
    -> , ifnull(value2,0) value2
    -> from (
    -> select tm.id, data, doc, sum(value) value1
    -> from t_master tm
    -> join t_transaksi_1 tr on tm.id=tr.id
    -> group by id, doc
    -> ) res1
    -> left join (
    -> select tm.id, data, doc, sum(value) value2
    -> from t_master tm
    -> join t_transaksi_2 tr on tm.id=tr.id
    -> group by id, doc
    -> ) res2 on res1.id=res2.id and res1.doc=res2.doc;
+----+------+-------+--------+--------+
| id | data | doc   | value1 | value2 |
+----+------+-------+--------+--------+
|  1 | A    | DOC 1 |   3000 |      0 |
|  2 | B    | DOC 2 |   5000 |   4000 |
|  3 | C    | DOC 3 |   3000 |   4000 |
|  3 | C    | DOC 4 |   5000 |   6000 |
+----+------+-------+--------+--------+
4 rows in set (0.00 sec)

```

Demikian TUTORIAL ini semoga membantu memahami penggunaan SUBQUERY, JOIN, GROUP BY, dan fungsi agregate SUM.


### Database Inventory

- Buat tabel `items`

```
MariaDB [inventory]> create table items (id serial primary key, items_id integer not null, code varchar(20) not null, name varchar(200) null);
Query OK, 0 rows affected (0.30 sec)

```
- Insert Items:

```
insert into items (code, name)
select 'ITEM01', 'Barang Pertama' union all
select 'ITEM02', 'Barang Kedua' union all
select 'ITEM03', 'Barang Ketiga';
```
- Buat table `item_balances` 

```
create table item_balances (
id serial primary key,
item_id integer not null,
period date not null,
quantity numeric(15,2),
unit_price numeric(15,2),
CONSTRAINT FOREIGN KEY (item_id) references items(items_id) );
```

```
alter table item_balances add constraint foreign key (item_id) references items(id);
```