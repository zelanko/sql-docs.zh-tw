---
title: ALTER DATABASE (Azure SQL 資料倉儲) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 2e89ba1dde52c1b5cb919ff34181d7ca723b6c61
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTER DATABASE (Azure SQL 資料倉儲)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

修改資料庫的名稱、大小上限或服務目標。  
  
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
使用指定為 *new_database_name* 的名稱來重新命名資料庫。  
  
MAXSIZE  
預設為 245,760 GB (240 TB)。  

**適用於：**最佳化彈性效能層級

資料庫的允許大小上限。 資料庫不可增大超過 MAXSIZE。 

**適用於：**最佳化計算效能層級

資料庫中資料列存放區資料的允許大小上限。 儲存在資料列存放區資料表的資料、資料行存放區索引的差異存放區，或叢集資料行存放區索引的非叢集索引，不可增大超過 MAXSIZE。  壓縮成資料行存放區格式的資料大小沒有大小限制，因此不受 MAXSIZE 限制。 
  
SERVICE_OBJECTIVE  
指定效能等級。 如需 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 服務目標的詳細資訊，請參閱[效能層級](https://azure.microsoft.com/documentation/articles/performance-tiers/)。  
  
## <a name="permissions"></a>Permissions  
需要下列權限：  
  
-   由佈建程序建立的伺服器層級主體登入，或  
  
-   `dbmanager` 資料庫角色的成員。  
  
除非資料庫擁有者是 `dbmanager` 角色的成員，否則無法變更資料庫。  
  
## <a name="general-remarks"></a>一般備註  
目前資料庫必須是與您變更的資料庫不同的資料庫，因此**必須在連線至 master 資料庫時執行 ALTER**。  
  
SQL 資料倉儲設定為 COMPATIBILITY_LEVEL 130，而且不可變更。 如需詳細資料，請參閱 [Azure SQL Database 中改善的查詢效能與相容性層級 130](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)。
  
若要縮小資料庫大小，請使用 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
若要執行 ALTER DATABASE，資料庫必須在線上，而且不能處於暫停狀態。  
  
ALTER DATABASE 陳述式必須以自動認可模式 (即預設交易管理模式) 執行。 這是設定於連線設定中。  
  
ALTER DATABASE 陳述式不能是使用者定義交易的一部分。

您無法變更資料庫定序。  
  
## <a name="examples"></a>範例  
執行這些範例之前，請確定您要變更的資料庫不是目前資料庫。 目前資料庫必須是與您變更的資料庫不同的資料庫，因此**必須在連線至 master 資料庫時執行 ALTER**。  

### <a name="a-change-the-name-of-the-database"></a>A. 變更資料庫的名稱  

```  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>B. 變更資料庫的大小上限  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>C. 變更效能等級  
  
```  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>D. 變更大小上限和效能等級  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>另請參閱  
[CREATE DATABASE (Azure SQL 資料倉儲)](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[SQL 資料倉儲參考主題清單](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  
