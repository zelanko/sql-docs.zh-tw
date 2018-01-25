---
title: "ALTER DATABASE （Azure SQL 資料倉儲） |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: "20"
author: barbkess
ms.author: barbkess
manager: craigg
ms.openlocfilehash: 71737beb817cfeebed195c90d056768aef678a3e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTER DATABASE （Azure SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

修改名稱、 大小上限或資料庫的服務目標。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ALTER DATABASE database_name  

  MODIFY NAME = new_database_name  
| MODIFY ( <edition_option> [, ... n] )  
  
<edition_option> ::=   
      MAXSIZE = { 
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 
          | 92160 | 102400 | 153600 | 204800 | 245760 
      } GB  
      | SERVICE_OBJECTIVE = { 
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' 
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' 
          | 'DW3000' | 'DW6000' | 'DW1000c' | 'DW1500c' | 'DW2000c' 
          | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c' | 'DW7500c' 
          | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }  
```  
  
## <a name="arguments"></a>引數  
*database_name*  
指定要修改的資料庫名稱。  

MODIFY NAME = *new_database_name*  
重新命名資料庫名稱指定為*new_database_name*。  
  
MAXSIZE  
預設值為 10240 GB (10 TB)。  

**適用於：**彈性效能層針對最佳化

資料庫的允許大小上限。 資料庫無法增長超過 MAXSIZE。 

**適用於：**針對計算效能層最佳化

在資料庫中的資料列存放區資料的可允許大小上限。 資料儲存在資料列存放區資料表、 資料行存放區索引的差異存放區或非叢集資料行存放區索引的非叢集索引不得成長超過 MAXSIZE。  壓縮成資料行存放區格式的資料不受限於 MAXSIZE，就不需要的大小限制。 
  
SERVICE_OBJECTIVE  
指定效能等級。 如需服務目標[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]，請參閱[效能層](https://azure.microsoft.com/documentation/articles/performance-tiers/)。  
  
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
  
