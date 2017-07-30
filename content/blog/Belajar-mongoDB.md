+++
title = "Tutorial MongoDB"
date = "2017-07-14T21:49:20+02:00"
tags = ["mysql", "mariaDB", "mongodb"]
categories = ["database"]
author = "tipobrata"
+++

## Contoh Database
```
{
	firstname:"dodot",
	lastname:"didit",
	memberships: ["mem1", "mem2"],
	address:{
			street: "jl. pramuka sokaraja",
			city:"banyumas"
	}
	contacts:[
			{name:"brath", relationship:"friend"},
	]
}
```

## Membuat Tabel

```
> use mycustomers
switched to db mycustomers
> db
mycustomers

```

## Membuat user

```
db.createUser({
		user:"didit",
		pwd:"12345",
		roles: ["readWrite", "dbAdmin"]
});

```

## Membuat collection / table

```
> db.createCollection('customers');

```

## Insert data ke collection customers

```
> db.customers.insert({first_name:"wirog", last_name:"sebastian"});
WriteResult({ "nInserted" : 1 })

```

## Insert 2 data

```
> db.customers.insert([{first_name:"kara", last_name:"matian"},{first_name:"dodol", lastname:"garut"}]);
BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 2,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})

```

## lihat isi collection customers

```
> db.customers.find();
{ "_id" : ObjectId("5968faf2a760ec2253e9120b"), "first_name" : "wirog", "last_name" : "sebastian" }
```

## lihat isi collection dengan pretty

```
> db.customers.find().pretty();
{
	"_id" : ObjectId("5968faf2a760ec2253e9120b"),
	"first_name" : "wirog",
	"last_name" : "sebastian"
}
{
	"_id" : ObjectId("5968fc37a760ec2253e9120c"),
	"first_name" : "kara",
	"last_name" : "matian"
}
{
	"_id" : ObjectId("5968fc37a760ec2253e9120d"),
	"first_name" : "dodol",
	"lastname" : "garut"
}
{
	"_id" : ObjectId("5968fd2ba760ec2253e9120e"),
	"first_name" : "kom",
	"last_name" : "tor"
}
{
	"_id" : ObjectId("5968fd2ba760ec2253e9120f"),
	"first_name" : "king",
	"lastname" : "soka",
	"gender" : "female"
}

```

## Merubah isi Collection / `$set`

```
> db.customers.update({first_name:"wirog"},{first_name:"wirog",last_name:"sebastian",gender:"male"});
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```
Atau dengan perintah di bawah bisa juga untuk menambah field baru:

```
> db.customers.update({first_name:"kara"},{$set:{gender:"male"}});
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```

## Menghapus field yang ada dalam collection / `$unset`

```
> db.customers.update({first_name:"kara"},{$unset:{age:1}});
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

```

## menambah nilai pada field age / `$inc`

```
> db.customers.update({first_name:"kara"},{$inc:{age:5}});
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

```

## Menambah field paling bawah.

```
> db.customers.update({first_name:"toy"},{first_name:"toy",last_name:"story"},{upsert: true});
WriteResult({
	"nMatched" : 0,
	"nUpserted" : 1,
	"nModified" : 0,
	"_id" : ObjectId("59690437c8e44c89532b5714")
})

```

## Rename nama field

```
> db.customers.update({first_name:"wirog"},{$rename:{"gender":"sex"}});
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

```
Hasil

```
//Sebelum
"_id" : ObjectId("5968faf2a760ec2253e9120b"),
	"first_name" : "wirog",
	"last_name" : "sebastian",
	"age" : 22,
	"gender" : "male"

//Sesudah
"_id" : ObjectId("5968faf2a760ec2253e9120b"),
	"first_name" : "wirog",
	"last_name" : "sebastian",
	"age" : 22,
	"sex" : "male"

```

## Hapus Berdasarkan ID

```
> db.customers.remove({first_name:"kom"});
WriteResult({ "nRemoved" : 1 })

```

## melihat jumlah data yang ada dalam collection

```
> db.customers.find().count();
5
```
