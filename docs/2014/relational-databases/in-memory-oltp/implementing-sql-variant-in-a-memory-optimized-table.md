---
title: 在記憶體最佳化資料表中實作 SQL_VARIANT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f17f21df-959d-4e20-92f3-bd707d555a46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: add4bbb072a91ad05d58d57f43821c441595afef
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58525840"
---
# <a name="implementing-sqlvariant-in-a-memory-optimized-table"></a>在記憶體最佳化資料表中實作 SQL_VARIANT
  請考量具有 `SQL_VARIANT` 資料行的資料表範例：  
  
```sql  
CREATE TABLE [dbo].[T1]([Key] [sql_variant] NOT NULL)  
```  
  
 假設索引鍵資料行只可以是 `BIGINT` 或 `NVARCHAR(300)`。 您可以依照下列方式製作此資料表的模型：  
  
```sql  
-- original disk-based table  
CREATE TABLE [dbo].[T1_disk]([Key] int not null primary key,  
       [Value] [sql_variant])  
go  
  
insert dbo.T1_disk values (1, 12345678)  
insert dbo.T1_disk values (2, N'my nvarchar')  
insert dbo.T1_disk values (3, NULL)  
go  
  
-- new memory-optimized table  
CREATE TABLE [dbo].[T1_inmem]([Key] INT NOT NULL PRIMARY KEY NONCLUSTERED,  
       [Value_bi] BIGINT,  
       [Value_nv] NVARCHAR(300),  
       [Value_enum] TINYINT NOT NULL) WITH (MEMORY_OPTIMIZED=ON)  
go  
  
-- copy data   
INSERT INTO dbo.T1_inmem  
  SELECT [Key],  
              CASE WHEN SQL_VARIANT_PROPERTY([Value], 'basetype') = 'bigint' THEN convert (bigint, [Value])  
              ELSE NULL END,  
              CASE WHEN SQL_VARIANT_PROPERTY([Value], 'basetype') != 'bigint' THEN convert (nvarchar(300), [Value])  
              ELSE NULL END,  
              CASE WHEN SQL_VARIANT_PROPERTY([Value], 'basetype') = 'bigint' THEN 1  
              ELSE 0 END  
  FROM dbo.T1_disk  
GO  
  
-- select data, converting back to sql_variant [will not work inside native proc]  
select [Key],   
       case [Value_enum] when 1 then convert(sql_variant, [Value_bi])   
    else convert(sql_variant, [Value_nv])   
    end  
from dbo.T1_inmem  
```  
  
 現在您可以藉由在從 T1 上開啟資料指標的方式，從 T1 將資料載入 [T1_HK] 中：  
  
```sql  
DECLARE T1_rows_cursor CURSOR FOR    
select *  
FROM dbo.T1  
  
OPEN T1_rows_cursor     
  
-- declare 1 variable each for column in HK table  
  
Declare  
@Key_biBIGINT = 0,  
@Key_nvnvarchar(300)= ' ',  
@Key_enumsmallint,  
@Keysql_variant  
  
FETCH NEXT FROM T1_rows_cursor INTO @key  
  
WHILE @@FETCH_STATUS = 0     
BEGIN     
  
-- setting the input parameters for inserting into the memory-optimized table  
-- convert SQL Variant types  
-- @key_enum =1 represents BIGINT  
if (SQL_VARIANT_PROPERTY(@Key, 'basetype') = 'bigint')  
begin  
set @key_bi = convert (bigint, @Key)  
set @key_enum = 1  
set @key_nv = 'invalid'  
end  
else  
begin  
set @Key_nv = convert (nvarchar (300), @Key)  
set @Key_enum = 0  
set @Key_bi = -1  
end  
  
-- inserting the row  
INSERT INTO T1_HK VALUES (@Key_bi, @Key_nv, @Key_enum)  
  
FETCH NEXT FROM T1_rows_cursor INTO @key  
END  
  
CLOSE T1_rows_cursor     
DEALLOCATE T1_rows_cursor  
```  
  
 您也可以將資料轉換回 `SQL_VARIANT`，如下所示：  
  
```sql  
case [Key_enum] when 1 then convert(sql_variant, [Key_bi])   
                       else convert(sql_variant, [Key_nv])   
                       end  
```  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  
