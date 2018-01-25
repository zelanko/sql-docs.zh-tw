---
title: "DBCC DROPCLEANBUFFERS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROPCLEANBUFFERS
- DBCC_DROPCLEANBUFFERS_TSQL
- DROPCLEANBUFFERS_TSQL
- DBCC DROPCLEANBUFFERS
dev_langs: TSQL
helpviewer_keywords:
- clean buffers
- cold buffer cache
- buffer pools [SQL Server]
- dropping buffers
- removing buffers
- DBCC DROPCLEANBUFFERS statement
ms.assetid: a4121927-f2ce-4926-aa2c-9b1519dac048
caps.latest.revision: "35"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aa4214f9bd043e31adb3f3e62340cbc023c9172d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

從緩衝集區和資料行存放區物件集區中的資料行存放區物件中移除所有的清除緩衝區。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法
SQL Server 的語法： 

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
Azure SQL 倉儲和 Parallel Data Warehouse 的語法：

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
 WITH NO_INFOMSGS  
 隱藏所有參考訊息。 參考用訊息一律會隱藏上[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
 COMPUTE  
 清除查詢計劃快取中的每個計算節點。  
  
 ALL  
 從每個計算節點和 [控制] 節點，請清除查詢計劃快取。 如果您未指定值，這是預設值。  
  
## <a name="remarks"></a>備註  
在不將伺服器關閉再重新啟動的情況下，可以使用 DBCC DROPCLEANBUFFERS，以冷緩衝快取區來測試查詢。
從緩衝集區和資料行存放區物件，從資料行存放區物件集區中卸除清除緩衝區，請先使用 CHECKPOINT 來產生冷緩衝快取。 此舉會強制將所有目前資料庫的中途分頁寫入磁碟中，然後清除緩衝區。 之後，您就可以發出 DBCC DROPCLEANBUFFERS 命令，從緩衝集區移除所有的緩衝區了。
  
## <a name="result-sets"></a>結果集  
在 DBCC DROPCLEANBUFFERS[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  

適用於： SQL Server、 Parallel Data Warehouse 

- 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  

適用對象：Azure SQL 資料倉儲

- 需要 DB_OWNER 固定的伺服器角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  
