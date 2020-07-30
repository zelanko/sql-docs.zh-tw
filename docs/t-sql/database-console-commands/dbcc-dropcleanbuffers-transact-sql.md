---
title: DBCC DROPCLEANBUFFERS (Transact-SQL)
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROPCLEANBUFFERS
- DBCC_DROPCLEANBUFFERS_TSQL
- DROPCLEANBUFFERS_TSQL
- DBCC DROPCLEANBUFFERS
dev_langs:
- TSQL
helpviewer_keywords:
- clean buffers
- cold buffer cache
- buffer pools [SQL Server]
- dropping buffers
- removing buffers
- DBCC DROPCLEANBUFFERS statement
ms.assetid: a4121927-f2ce-4926-aa2c-9b1519dac048
author: pmasl
ms.author: umajay
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 68e9eca249d976398618a63e25b98c02dcf7f806
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394303"
---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS (Transact-SQL)

[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

移除緩衝集區中的所有清除緩衝區，以及移除資料行存放區物件集區中的資料行存放區物件。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法
SQL Server 的語法：

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
Azure SQL 資料倉儲和平行處理資料倉儲的語法：

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```

## <a name="arguments"></a>引數  
 WITH NO_INFOMSGS  
 隱藏所有參考訊息。 在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 上一律會隱藏參考訊息。  
  
 COMPUTE  
 從每個計算節點中，清除記憶體中的資料快取。  
  
 ALL  
 從每個計算節點和控制節點中，清除記憶體中的資料快取。 如果您未指定值，則這是預設值。  
  
## <a name="remarks"></a>備註  
在不將伺服器關閉再重新啟動的情況下，可以使用 DBCC DROPCLEANBUFFERS，以冷緩衝快取區來測試查詢。
若要從緩衝集區中卸除清除緩衝區，以及從資料行存放區物件集區中卸除資料行存放區物件，請先使用 CHECKPOINT 來產生冷緩衝區快取。 此舉會強制將所有目前資料庫的中途分頁寫入磁碟中，然後清除緩衝區。 之後，您就可以發出 DBCC DROPCLEANBUFFERS 命令，從緩衝集區移除所有的緩衝區了。
  
## <a name="result-sets"></a>結果集  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的 DBCC DROPCLEANBUFFERS 會傳回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>權限  

適用對象：SQL Server、平行處理資料倉儲 

- 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  

適用對象：Azure SQL 資料倉儲

- 需要 DB_OWNER 固定資料庫角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  
