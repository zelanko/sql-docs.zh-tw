---
title: "ALTER DATABASE （Azure SQL 資料倉儲） |Microsoft 文件"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 03/03/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: 20
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b5e328da952c853409437f7c3a4993f17022de22
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTER DATABASE （Azure SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

修改名稱、 大小上限或資料庫的服務目標。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
ALTER DATABASE database_name  

  MODIFY NAME = new_database_name  
| MODIFY ( <edition_option> [, ... n] )  
  
<edition_option> ::=   
      MAXSIZE = { 250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 | 153600 | 204800 | 245760 } GB  
    | SERVICE_OBJECTIVE = { 'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000'}  
```  
  
## <a name="arguments"></a>引數  
*database_name*  
指定要修改的資料庫名稱。  

MODIFY NAME = *new_database_name*  
重新命名資料庫名稱指定為*new_database_name*。  
  
MAXSIZE  
資料庫的最大可以增長至。 設定此值可防止大小設定超過資料庫大小的成長。 預設值*MAXSIZE*時未指定為 10240 GB (10 TB)。 其他可能的值範圍從 250 GB 最多 240 TB。  
  
SERVICE_OBJECTIVE  
指定效能等級。 如需服務目標[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]，請參閱[SQL 資料倉儲上的小數位數效能](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-manage-compute-overview/)。  
  
## <a name="permissions"></a>Permissions  
需要這些權限：  
  
-   伺服器層級主體登入 （由佈建程序建立一個），或  
  
-   成員的`dbmanager`資料庫角色。  
  
資料庫的擁有者不能改變資料庫，除非擁有者是屬於`dbmanager`角色。  
  
## <a name="general-remarks"></a>一般備註  
目前的資料庫必須是不同的資料庫，您會改變，因此比**連接到 master 資料庫時，就必須執行 ALTER**。  
  
SQL 資料倉儲設定為 COMPATIBILITY_LEVEL 130，而且無法變更。 如需詳細資訊，請參閱[改善查詢效能與 Azure SQL Database 中的相容性層級 130](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)。
  
若要減少資料庫大小，請使用[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
若要執行 ALTER DATABASE，資料庫必須在線上，且不能處於暫停狀態。  
  
ALTER DATABASE 陳述式必須在自動認可模式，這是預設交易管理模式執行。 這是設定的連線設定。  
  
ALTER DATABASE 陳述式不能是使用者定義交易的一部分。

您無法變更資料庫定序。  
  
## <a name="examples"></a>範例  
執行這些範例之前，請確定會改變的資料庫不是目前的資料庫。 目前的資料庫必須是不同的資料庫，您會改變，因此比**連接到 master 資料庫時，就必須執行 ALTER**。  

### <a name="a-change-the-name-of-the-database"></a>A. 變更資料庫的名稱  

```  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>B. 變更資料庫的大小上限  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>C. 變更效能層級  
  
```  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>D. 變更大小上限和效能層級  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>另請參閱  
[CREATE DATABASE （Azure SQL 資料倉儲）](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[SQL 資料倉儲清單的參考主題](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  
