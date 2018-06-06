---
title: 路徑名稱 (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PathName_TSQL
- PathName
dev_langs:
- TSQL
helpviewer_keywords:
- PathName FILESTREAM [SQL Server]
ms.assetid: 6b95ad90-6c82-4a23-9294-a2adb74934a3
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 80fc13baa2d538e054ed88607cd4b45c6477cb6e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="pathname-transact-sql"></a>PathName (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 FILESTREAM 二進位大型物件 (BLOB) 的路徑。 OpenSqlFilestream API 會傳回的控制代碼的應用程式可以使用 Win32 api 處理 BLOB 資料，使用此路徑。 PathName 是唯讀的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
column_name.PathName ( @option [ , use_replica_computer_name ] )  
```  
  
## <a name="arguments"></a>引數  
 *column_name*  
 資料行名稱**varbinary （max)** FILESTREAM 資料行。 *column_name*必須是資料行名稱。 它不能是運算式或是 CAST 或 CONVERT 陳述式的結果。  
  
 要求的資料行的任何其他資料型別或 PathName **varbinary （max)** columnthat 沒有 FILESTREAM 儲存體屬性會導致查詢編譯時間錯誤。  
  
 *@option*  
 整數[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，定義路徑的伺服器元件應如何格式化。 *@option* 可以是下列值之一。 預設值是 0。  
  
|Value|설명|  
|-----------|-----------------|  
|0|傳回轉換成 BIOS 格式的伺服器名稱，例如：`\\SERVERNAME\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F19F7-38EA-4AB0-BB89-E6C545DBD3F9`|  
|1|在不轉換的情況下傳回伺服器名稱，例如：`\\ServerName\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F1`|  
|2|傳回完整伺服器路徑，例如：`\\ServerName.MyDomain.com\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F19F7-38EA-4AB0-BB89-E6C545DBD3F9`|  
  
 *use_replica_computer_name*  
 定義的伺服器名稱應如何傳回 Always On 可用性群組中的位元值。  
  
 當資料庫不屬於 Alwayson 可用性群組時，則會忽略這個引數的值。 電腦名稱一定會用於路徑中。  
  
 當資料庫屬於 Alwayson 可用性群組時，值*use_replica_computer_name*有下列的輸出效果**PathName**函式：  
  
|Value|Description|  
|-----------|-----------------|  
|未指定。|此函數會傳回路徑中的虛擬網路名稱 (VNN)。|  
|0|此函數會傳回路徑中的虛擬網路名稱 (VNN)。|  
|1|此函數會傳回路徑中的電腦名稱。|  
  
## <a name="return-type"></a>傳回類型  
 **nvarchar(max)**  
  
## <a name="return-value"></a>傳回值  
 傳回的值是 BLOB 的完整邏輯路徑或 NETBIOS 路徑。 PathName 不會傳回 IP 位址。 尚未建立 FILESTREAM BLOB 時，便會傳回 NULL。  
  
## <a name="remarks"></a>備註  
 必須可以在呼叫 PathName 的任何查詢中看到 ROWGUID 資料行。  
  
 只能使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建立 FILESTREAM BLOB。  
  
## <a name="examples"></a>範例  
  
### <a name="a-reading-the-path-for-a-filestream-blob"></a>A. 讀取 FILESTREAM BLOB 的路徑  
 下列範例會將 `PathName` 指派給 `nvarchar(max)` 變數。  
  
```sql  
DECLARE @PathName nvarchar(max);  
SET @PathName = (  
    SELECT TOP 1 photo.PathName()  
    FROM dbo.Customer  
    WHERE LastName = 'CustomerName'  
    );  
```  
  
### <a name="b-displaying-the-paths-for-filestream-blobs-in-a-table"></a>B. 顯示資料表中的 FILESTREAM BLOB 路徑  
 下列範例會建立及顯示三個 FILESTREAM BLOB 的路徑。  
  
```sql  
-- Create a FILESTREAM-enabled database.  
-- The c:\data directory must exist.  
CREATE DATABASE PathNameDB  
ON  
PRIMARY ( NAME = ArchX1,  
    FILENAME = 'c:\data\archdatP1.mdf'),  
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = ArchX3,  
    FILENAME = 'c:\data\filestreamP1')  
LOG ON  ( NAME = ArchlogX1,  
    FILENAME = 'c:\data\archlogP1.ldf');  
GO  
  
USE PathNameDB;  
GO  
  
-- Create a table, add some records, and  
-- create the associated FILESTREAM  
-- BLOB files.  
  
CREATE TABLE TABLE1  
    (  
        ID int,  
        RowGuidColumn UNIQUEIDENTIFIER  
                      NOT NULL UNIQUE ROWGUIDCOL,  
        FILESTREAMColumn varbinary(MAX) FILESTREAM  
    );  
GO  
  
INSERT INTO TABLE1 VALUES  
 (1, NEWID(), 0x00)  
,(2, NEWID(), 0x00)  
,(3, NEWID(), 0x00);  
GO  
  
SELECT FILESTREAMColumn.PathName() AS 'PathName' FROM TABLE1;  
  
--Results  
--PathName  
------------------------------------------------------------------------------------------------------------  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\DD67C792-916E-4A76-8C8A-4A85DC5DB908  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\2907122B-2560-4CB9-86DC-FBE7ABA1843B  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\922BE0E0-CAB9-4403-90BF-945BD258E4BC  
--  
--(3 row(s) affected)  
GO  
  
--Drop the database to clean up.  
USE master;  
GO  
DROP DATABASE PathNameDB;  
```  
  
## <a name="see-also"></a>另請參閱  
 [二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [GET_FILESTREAM_TRANSACTION_CONTEXT &#40;Transact SQL&#41;](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md)   
 [使用 OpenSqlFilestream 存取 FILESTREAM 資料](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
  
