---
title: SQL Graph 資料庫範例 |Microsoft Docs
description: 快速範例可協助您開始使用 SQL graph 資料庫中引進的新語法。
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, tsql reference
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 24dd60c0341bc3f32192a5ac94fe786e9483a9f0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480119"
---
# <a name="create-a-graph-database-and-run-some-pattern-matching-queries-using-t-sql"></a>使用 T-sql 建立圖形資料庫並執行一些模式比對查詢

[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

這個範例會提供一個 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 腳本，用來建立具有節點和邊緣的圖形資料庫，然後使用新的 MATCH 子句來比對某些模式並跨越圖形。 此範例腳本適用于 Azure SQL Database 和 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]  

## <a name="sample-schema"></a>範例架構

此範例會針對具有人員、餐廳和城市節點的假設社交網路，建立圖表架構（如圖1所示）。 這些節點會使用朋友、贊、LivesIn 和 LocatedIn 邊緣彼此連接。

![此圖顯示具有餐廳、city、person 節點和 LivesIn、LocatedIn、贊邊的範例架構。](../../relational-databases/graphs/media/person-cities-restaurants-tables.png "Sql graph 資料庫範例")  
圖1：使用餐廳、city、person 節點和 LivesIn、LocatedIn、贊邊的範例架構。

## <a name="sample-script"></a>範例指令碼

```
-- Create a graph demo database
IF NOT EXISTS (SELECT * FROM sys.databases WHERE NAME = 'graphdemo')
    CREATE DATABASE GraphDemo;
GO

USE GraphDemo;
GO

-- Create NODE tables
CREATE TABLE Person (
  ID INTEGER PRIMARY KEY,
  name VARCHAR(100)
) AS NODE;

CREATE TABLE Restaurant (
  ID INTEGER NOT NULL,
  name VARCHAR(100),
  city VARCHAR(100)
) AS NODE;

CREATE TABLE City (
  ID INTEGER PRIMARY KEY,
  name VARCHAR(100),
  stateName VARCHAR(100)
) AS NODE;

-- Create EDGE tables. 
CREATE TABLE likes (rating INTEGER) AS EDGE;
CREATE TABLE friendOf AS EDGE;
CREATE TABLE livesIn AS EDGE;
CREATE TABLE locatedIn AS EDGE;

-- Insert data into node tables. Inserting into a node table is same as inserting into a regular table
INSERT INTO Person (Id, name)
    VALUES (1, 'John')
         , (2, 'Mary')
         , (3, 'Alice')
         , (4, 'Jacob')
         , (5, 'Julie');

INSERT INTO Restaurant (Id, name, city)
    VALUES (1, 'Taco Dell','Bellevue')
         , (2, 'Ginger and Spice','Seattle')
         , (3, 'Noodle Land', 'Redmond');

INSERT INTO City (Id, name, stateName)
    VALUES (1,'Bellevue','wa')
         , (2,'Seattle','wa')
         , (3,'Redmond','wa');

-- Insert into edge table. While inserting into an edge table,
-- you need to provide the $node_id from $from_id and $to_id columns.
/* Insert which restaurants each person likes */
INSERT INTO likes 
    VALUES ((SELECT $node_id FROM Person WHERE ID = 1), (SELECT $node_id FROM Restaurant WHERE ID = 1), 9)
         , ((SELECT $node_id FROM Person WHERE ID = 2), (SELECT $node_id FROM Restaurant WHERE ID = 2), 9)
         , ((SELECT $node_id FROM Person WHERE ID = 3), (SELECT $node_id FROM Restaurant WHERE ID = 3), 9)
         , ((SELECT $node_id FROM Person WHERE ID = 4), (SELECT $node_id FROM Restaurant WHERE ID = 3), 9)
         , ((SELECT $node_id FROM Person WHERE ID = 5), (SELECT $node_id FROM Restaurant WHERE ID = 3), 9);

/* Associate in which city live each person*/
INSERT INTO livesIn 
    VALUES ((SELECT $node_id FROM Person WHERE ID = 1), (SELECT $node_id FROM City WHERE ID = 1))
         , ((SELECT $node_id FROM Person WHERE ID = 2), (SELECT $node_id FROM City WHERE ID = 2))
         , ((SELECT $node_id FROM Person WHERE ID = 3), (SELECT $node_id FROM City WHERE ID = 3))
         , ((SELECT $node_id FROM Person WHERE ID = 4), (SELECT $node_id FROM City WHERE ID = 3))
         , ((SELECT $node_id FROM Person WHERE ID = 5), (SELECT $node_id FROM City WHERE ID = 1));

/* Insert data where the restaurants are located */
INSERT INTO locatedIn 
    VALUES ((SELECT $node_id FROM Restaurant WHERE ID = 1), (SELECT $node_id FROM City WHERE ID =1))
         , ((SELECT $node_id FROM Restaurant WHERE ID = 2), (SELECT $node_id FROM City WHERE ID =2))
         , ((SELECT $node_id FROM Restaurant WHERE ID = 3), (SELECT $node_id FROM City WHERE ID =3));

/* Insert data into the friendOf edge */
INSERT INTO friendOf 
    VALUES ((SELECT $NODE_ID FROM Person WHERE ID = 1), (SELECT $NODE_ID FROM Person WHERE ID = 2))
         , ((SELECT $NODE_ID FROM Person WHERE ID = 2), (SELECT $NODE_ID FROM Person WHERE ID = 3))
         , ((SELECT $NODE_ID FROM Person WHERE ID = 3), (SELECT $NODE_ID FROM Person WHERE ID = 1))
         , ((SELECT $NODE_ID FROM Person WHERE ID = 4), (SELECT $NODE_ID FROM Person WHERE ID = 2))
         , ((SELECT $NODE_ID FROM Person WHERE ID = 5), (SELECT $NODE_ID FROM Person WHERE ID = 4));


-- Find Restaurants that John likes
SELECT Restaurant.name
FROM Person, likes, Restaurant
WHERE MATCH (Person-(likes)->Restaurant)
AND Person.name = 'John';

-- Find Restaurants that John's friends like
SELECT Restaurant.name 
FROM Person person1, Person person2, likes, friendOf, Restaurant
WHERE MATCH(person1-(friendOf)->person2-(likes)->Restaurant)
AND person1.name='John';

-- Find people who like a restaurant in the same city they live in
SELECT Person.name
FROM Person, likes, Restaurant, livesIn, City, locatedIn
WHERE MATCH (Person-(likes)->Restaurant-(locatedIn)->City AND Person-(livesIn)->City);
```

## <a name="clean-up"></a>清除  
清除針對此範例所建立的架構和資料庫。

```
USE graphdemo;
go

DROP TABLE IF EXISTS likes;
DROP TABLE IF EXISTS Person;
DROP TABLE IF EXISTS Restaurant;
DROP TABLE IF EXISTS City;
DROP TABLE IF EXISTS friendOf;
DROP TABLE IF EXISTS livesIn;
DROP TABLE IF EXISTS locatedIn;

USE master;
go
DROP DATABASE graphdemo;
go
```

## <a name="script-explanation"></a>指令碼說明  
此腳本會使用新的 T-sql 語法來建立節點和邊緣資料表。 示範如何使用語句，將資料插入至節點和邊緣資料表 `INSERT` ，也會示範如何使用 `MATCH` 子句進行模式比對和導覽。

|Command    |注意
|---  |---  |
|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)  |建立圖形節點或邊緣資料表  |
|[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)  |插入至節點或邊緣資料表  |
|[&#40;Transact-sql&#41;相符 ](../../t-sql/queries/match-sql-graph.md)  |使用 MATCH 來比對模式或跨越圖形  |
