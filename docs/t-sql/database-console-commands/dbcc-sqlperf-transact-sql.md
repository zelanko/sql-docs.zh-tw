---
title: DBCC SQLPERF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQLPERF
- DBCC_SQLPERF_TSQL
- SQLPERF_TSQL
- DBCC SQLPERF
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], transaction logs
- transaction logs [SQL Server], space usage
- space [SQL Server], transaction logs
- DBCC SQLPERF statement
ms.assetid: ec9225ce-e20f-4b03-8b3a-7bcad8a649df
author: pmasl
ms.author: umajay
ms.openlocfilehash: baa77f853e048fdc1098a93ae7036fd927efbe9c
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485550"
---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

為所有資料庫提供交易記錄空間使用量的統計資料。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，它可以用來重設等候及閂鎖統計資料。
  
**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本)、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([在某些區域中為預覽版本](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     | [ "sys.dm_os_latch_stats" , CLEAR ]  
     | [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
LOGSPACE  
傳回目前交易記錄大小以及用於每一個資料庫的記錄空間百分比。 使用這些資訊可以監視交易記錄中所用的空間量。

> [!IMPORTANT]
> 如需從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 起有關交易記錄空間使用量資訊的詳細資訊，請參閱本主題中的[備註](#Remarks)一節。
  
**"sys.dm_os_latch_stats"** , CLEAR  
重設閂鎖統計資料。 如需詳細資訊，請參閱 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)。 此選項在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中無法使用。  
  
**"sys.dm_os_wait_stats"** , CLEAR  
重設等候統計資料。 如需詳細資訊，請參閱 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。 此選項在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中無法使用。  
  
WITH NO_INFOMSGS  
抑制所有嚴重性層級在 0 到 10 的參考用訊息。  
  
## <a name="result-sets"></a>結果集  
 下表描述結果集中的資料行。  
  
|資料行名稱|定義|  
|---|---|
|**Database Name**|顯示記錄統計資料的資料庫名稱。|  
|**記錄大小 (MB)**|目前配置給記錄的大小。 這個值一定會比原先配置給記錄空間的量小，因為 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會保留少量內部標頭資訊所用的磁碟空間。|  
|**所用的記錄空間 (%)**|記錄檔目前使用於儲存交易記錄資訊的百分比。|  
|**狀態**|記錄檔的狀態。 一律是 0。|  
  
## <a name="remarks"></a><a name="Remarks"></a> 備註  
從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，請使用 [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) DMV 取代 `DBCC SQLPERF(LOGSPACE)` 來傳回每個資料庫交易記錄的空間使用量資訊。    
 
交易記錄會記錄資料庫中所做的每一筆交易。 如需詳細資訊，請參閱[交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) 與 [SQL Server 交易記錄架構與管理指南](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)。
  
## <a name="permissions"></a>權限  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上執行 `DBCC SQLPERF(LOGSPACE)` 需要伺服器的 `VIEW SERVER STATE` 權限。 若要重設等候和閂鎖統計資料，需要伺服器的 `ALTER SERVER STATE` 權限。
  
在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 進階和業務關鍵層上需要資料庫中的 `VIEW DATABASE STATE` 權限。 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 標準、基本，和一般用途層上需要 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 系統管理員帳戶。 不支援重設等候和閂鎖統計資料。
  
## <a name="examples"></a>範例  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. 顯示所有資料庫的記錄檔空間資訊  
下列範例會顯示包含在 `LOGSPACE` 執行個體內之所有資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資訊。
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Database Name Log Size (MB) Log Space Used (%) Status        
------------- ------------- ------------------ -----------   
master         3.99219      14.3469            0   
tempdb         1.99219      1.64216            0   
model          1.0          12.7953            0   
msdb           3.99219      17.0132            0   
AdventureWorks 19.554688    17.748701          0  
```  
  
### <a name="b-resetting-wait-statistics"></a>B. 重設等待統計資料  
下列範例會重設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的等待統計資料。
  
```sql  
DBCC SQLPERF("sys.dm_os_wait_stats",CLEAR);  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
[sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)    
[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)    
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)     
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)     

