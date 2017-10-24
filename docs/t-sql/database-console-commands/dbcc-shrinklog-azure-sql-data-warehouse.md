---
title: "DBCC SHRINKLOG （Azure SQL 資料倉儲） |Microsoft 文件"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f572bdbf8a0606c6652de4838b7b72664040156a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-shrinklog-azure-sql-data-warehouse"></a>DBCC SHRINKLOG （Azure SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

減少交易記錄檔的大小*跨設備*目前[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫。 資料是以壓縮交易記錄檔磁碟重組。 經過一段時間，在資料庫交易記錄可能會變得分散和效率不佳。 使用 DBCC SHRINKLOG 來減少片段化並減少記錄檔大小。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>引數  
大小 = { *target_size* [MB |**GB** |TB]} |**預設**。  
*target_size* DBCC SHRINKLOG 完成之後，所有計算節點，都則所需的交易記錄檔大小。 它是大於 0 的整數。  
記錄檔大小是以 (mb)、 (gb) 或 tb 為單位。 它是交易記錄檔的所有計算節點上的合併的大小。  
根據預設，DBCC SHRINKLOG 降低交易記錄檔儲存在資料庫的中繼資料中的記錄檔大小。 中繼資料中的記錄檔大小由在 LOG_SIZE 參數[CREATE DATABASE &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)或[ALTER DATABASE &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md). DBCC SHRINKLOG 可交易記錄大小減少為預設值時`SIZE=DEFAULT`指定，或當`SIZE`省略子句。
  
WITH NO_INFOMSGS  
DBCC SHRINKLOG 結果中，不會顯示參考用訊息。  
  
## <a name="permissions"></a>Permissions  
需要 ALTER SERVER STATE 權限。
  
## <a name="general-remarks"></a>一般備註  
DBCC SHRINKLOG 不會變更儲存在資料庫的中繼資料中的記錄檔大小。 中繼資料會繼續包含 CREATE DATABASE 或 ALTER DATABASE 陳述式中指定了 LOG_SIZE 參數。
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>A. 壓縮交易記錄所建立的資料庫指定的原始大小。  
假設位址資料庫建立時，位址資料庫的交易記錄檔已設定為 100 MB。 也就是位址的 CREATE DATABASE 陳述式有 LOG_SIZE = 100 MB。 現在，假設記錄成長過為 150MB，而且您想要壓縮回到 100 MB。
  
每個下列陳述式會嘗試將位址資料庫的交易記錄檔壓縮為 100 mb 的預設大小。 如果壓縮到 100 MB 的記錄將會導致資料遺失，DBCC SHRINKLOG 將會壓縮記錄檔到大小最小，大於 100 MB，而不會遺失資料。
  
```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```  
  
  

