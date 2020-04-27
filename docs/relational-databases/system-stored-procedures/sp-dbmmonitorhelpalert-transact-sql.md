---
title: sp_dbmmonitorhelpalert （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorhelpalert_TSQL
- sp_dbmmonitorhelpalert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorhelpalert
- database mirroring [SQL Server], monitoring
ms.assetid: 43911660-b4e4-4934-8c02-35221160aaec
author: stevestein
ms.author: sstein
ms.openlocfilehash: fc850c8be9b5222fe178563de78e34e2ba263c12
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899183"
---
# <a name="sp_dbmmonitorhelpalert-transact-sql"></a>sp_dbmmonitorhelpalert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關其中一個或所有關鍵資料庫鏡像監視器效能標準之警告臨界值的資訊。  
 
  ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbmmonitorhelpalert database_name   
    [ , alert_id ]   
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 指定資料庫。  
  
 [ *alert_id* ]  
 識別要傳回之警告的整數值。 如果省略這個引數，就會傳回所有的警告，但不會傳回保留期限。  
  
 若要傳回特定的警告，請指定下列其中一個值：  
  
|值|效能標準|警告臨界值|  
|-----------|------------------------|-----------------------|  
|1|最舊尚未傳送的交易|指定在主體伺服器執行個體上產生警告之前，傳送佇列中可以累積的交易分鐘數。 這項警告有助於根據時間來衡量可能的資料遺失，而且與高效能模式特別有相關性。 但是，當鏡像因為夥伴中斷連接而暫停或暫止時，這個警告也會與高安全性模式有關。|  
|2|未傳送的記錄|指定會在主體伺服器執行個體上產生警告之未傳送記錄的 KB 數。 這項警告有助於根據 KB 來衡量可能的資料遺失，而且與高效能模式特別有相關性。 但是，當鏡像因為夥伴中斷連接而暫停或暫止時，這個警告也會與高安全性模式有關。|  
|3|未還原的記錄|指定會在鏡像伺服器執行個體上產生警告之未還原記錄的 KB 數。 這個警告有助於測量容錯移轉時間。 *容錯移轉時間* 主要包含先前的鏡像伺服器向前復原其重做佇列中剩餘之所有記錄所需的時間，再加上一段很短的額外時間。|  
|4|鏡像認可負擔|指定在主體伺服器上產生警告之前所容許之每項交易的平均延遲毫秒數。 這項延遲是當主體伺服器執行個體等待鏡像伺服器執行個體將交易記錄寫入重做佇列中時所產生的負擔量。 只有在高安全性模式中才會顯出這個值的重要性。|  
|5|保留期限|在資料庫鏡像狀態資料表中控制資料列保留時間的中繼資料。|  
  
 如需對應于警告的事件識別碼的詳細資訊，請參閱[&#40;SQL Server&#41;，使用鏡像效能標準的警告臨界值和警示](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
 針對每個傳回的警示，傳回包含下列資料行的資料列：  
  
|資料行|資料類型|描述|  
|------------|---------------|-----------------|  
|**alert_id**|**int**|下表列出每個效能標準的**alert_id**值，以及**sp_dbmmonitorresults**結果集中顯示的度量單位度量：|  
|**閾值**|**int**|警告的臨界值。 如果在更新鏡像狀態時，傳回了這個臨界值以上的值，會在 Windows 事件記錄檔中輸入一個項目。 根據警告而定，這個值可能代表 KB、分鐘或毫秒。 如果目前尚未設定臨界值，則此值為 NULL。<br /><br /> **注意：** 若要查看目前的值，請執行[sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)預存程式。|  
|**後**|**bit**|0 = 事件已停用。<br /><br /> 1 = 事件已啟用。<br /><br /> **注意：** 保留期限一律為啟用狀態。|  
  
|值|效能標準|單位|  
|-----------|------------------------|----------|  
|1|最舊尚未傳送的交易|分鐘|  
|2|未傳送的記錄|KB|  
|3|未還原的記錄|KB|  
|4|鏡像認可負擔|毫秒|  
|5|保留期限|小時|  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會傳回資料列，指出是否已在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫上啟用尚未傳送之最舊交易效能標準的警告。  
  
```  
EXEC sp_dbmmonitorhelpalert AdventureWorks2012, 1 ;  
```  
  
 下列範例會針對每個效能標準傳回資料列，指出是否已在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫上啟用該標準。  
  
```  
EXEC sp_dbmmonitorhelpalert AdventureWorks2012;  
```  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
