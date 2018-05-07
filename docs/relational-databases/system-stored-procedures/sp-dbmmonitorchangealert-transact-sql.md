---
title: sp_dbmmonitorchangealert (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorchangealert_TSQL
- sp_dbmmonitorchangealert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorchangealert
- database mirroring [SQL Server], monitoring
ms.assetid: 1b29f82b-9cf8-4539-8d5c-9a1024db8a50
caps.latest.revision: 42
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8eb29c4aba54f2db1421fcc4de83322c2f37c3d6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spdbmmonitorchangealert-transact-sql"></a>sp_dbmmonitorchangealert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  加入或變更指定之鏡像效能標準的警告臨界值。  

  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbmmonitorchangealert database_name   
    , alert_id   
    , alert_threshold   
    , enabled   
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 指定要為其加入或變更指定之警告臨界值的資料庫。  
  
 *alert_id*  
 識別要加入或變更之警告的整數值。 指定下列其中一個值：  
  
|Value|效能標準|警告臨界值|  
|-----------|------------------------|-----------------------|  
|1|最舊尚未傳送的交易|指定在主體伺服器執行個體上產生警告之前，傳送佇列中可以累積的交易分鐘數。 這項警告有助於根據時間來衡量可能的資料遺失，而且與高效能模式特別有相關性。 但是，當鏡像因為夥伴中斷連接而暫停或暫止時，這個警告也會與高安全性模式有關。|  
|2|未傳送的記錄|指定會在主體伺服器執行個體上產生警告之未傳送記錄的 KB 數。 這項警告有助於根據 KB 來衡量可能的資料遺失，而且與高效能模式特別有相關性。 但是，當鏡像因為夥伴中斷連接而暫停或暫止時，這個警告也會與高安全性模式有關。|  
|3|未還原的記錄|指定會在鏡像伺服器執行個體上產生警告之未還原記錄的 KB 數。 這個警告有助於測量容錯移轉時間。 *容錯移轉時間* 主要包含先前的鏡像伺服器向前復原其重做佇列中剩餘之所有記錄所需的時間，再加上一段很短的額外時間。|  
|4|鏡像認可負擔|指定在主體伺服器上產生警告之前所容許之每項交易的平均延遲毫秒數。 這項延遲是當主體伺服器執行個體等待鏡像伺服器執行個體將交易記錄寫入重做佇列中時所產生的負擔量。 只有在高安全性模式中才會顯出這個值的重要性。|  
|5|保留期限|在資料庫鏡像狀態資料表中控制資料列保留時間的中繼資料。|  
  
 如需這些警告相對應的事件識別碼資訊，請參閱[使用警告臨界值與警示鏡像效能標準&#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)。  
  
 *alert_threshold*  
 警告的臨界值。 如果在更新鏡像狀態時，傳回了這個臨界值以上的值，會在 Windows 事件記錄檔中輸入一個項目。 根據效能標準而定，這個值可能代表 KB、分鐘或毫秒。  
  
> [!NOTE]  
>  若要檢視目前的值，請執行[sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)預存程序。  
  
 *enabled*  
 是否已啟用警告？  
  
 0 = 警告已停用。  
  
 1 = 警告已啟用。  
  
> [!NOTE]  
>  一定會啟用保留期限。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會為 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫設定每個效能標準的臨界值及保留期限。 下表顯示範例中所使用的值。  
  
|*alert_id*|效能標準|警告臨界值|是否已啟用警告？|  
|-----------------|------------------------|-----------------------|-----------------------------|  
|1|最舊尚未傳送的交易|30 分鐘|是|  
|2|未傳送的記錄|10000 KB|是|  
|3|未還原的記錄|10000 KB|是|  
|4|鏡像認可負擔|1,000 毫秒|否|  
|5|保留期限|8 小時|是|  
  
```  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 1, 30, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 2, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 3, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 4, 1000, 0 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 5, 8, 1 ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorhelpalert &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
  
