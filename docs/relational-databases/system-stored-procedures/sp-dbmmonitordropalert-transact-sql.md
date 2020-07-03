---
title: sp_dbmmonitordropalert （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitordropalert_TSQL
- sp_dbmmonitordropalert
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], monitoring
- sp_dbmmonitordropalert
ms.assetid: fe4a134b-25bf-464e-a5c4-358de215b65a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 00841f918a5b93b0ae27f907bff263f4c0a0174a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85866378"
---
# <a name="sp_dbmmonitordropalert-transact-sql"></a>sp_dbmmonitordropalert (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將臨界值設定為 NULL，發出指定效能標準的警告。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbmmonitordropalert database_name   
    [ , alert_id ]   
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 指定要發出其指定警告臨界值的資料庫。  
  
 *alert_id*  
 識別要發出之警告的整數值。 如果省略這個引數，將會發出資料庫上的所有警告。 若要發出特定效能標準的警告，請指定下列其中一個值：  
  
|值|效能標準|警告臨界值|  
|-----------|------------------------|-----------------------|  
|1|最舊尚未傳送的交易|指定在主體伺服器執行個體上產生警告之前，傳送佇列中可以累積的交易分鐘數。 這項警告有助於根據時間來衡量可能的資料遺失，而且與高效能模式特別有相關性。 但是，當鏡像因為夥伴中斷連接而暫停或暫止時，這個警告也會與高安全性模式有關。|  
|2|未傳送的記錄|指定會在主體伺服器執行個體上產生警告之未傳送記錄的 KB 數。 這項警告有助於根據 KB 來衡量可能的資料遺失，而且與高效能模式特別有相關性。 但是，當鏡像因為夥伴中斷連接而暫停或暫止時，這個警告也會與高安全性模式有關。|  
|3|未還原的記錄|指定會在鏡像伺服器執行個體上產生警告之未還原記錄的 KB 數。 這個警告有助於測量容錯移轉時間。 *容錯移轉時間* 主要包含先前的鏡像伺服器向前復原其重做佇列中剩餘之所有記錄所需的時間，再加上一段很短的額外時間。|  
|4|鏡像認可負擔|指定在主體伺服器上產生警告之前所容許之每項交易的平均延遲毫秒數。 這項延遲是當主體伺服器執行個體等待鏡像伺服器執行個體將交易記錄寫入重做佇列中時所產生的負擔量。 只有在高安全性模式中才會顯出這個值的重要性。|  
|5|保留期限|在資料庫鏡像狀態資料表中控制資料列保留時間的中繼資料。|  
  
> [!NOTE]  
>  不論是使用**sp_dbmmonitorchangealert**或「資料庫鏡像監視器」來指定，此程式都會捨棄警告臨界值。  
  
 如需對應于警告的事件識別碼的詳細資訊，請參閱[&#40;SQL Server&#41;，使用鏡像效能標準的警告臨界值和警示](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會發出 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的保留期限設定。  
  
```  
EXEC sp_dbmmonitordropalert AdventureWorks2012, 5;  
```  
  
 下列範例會發出 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的保留期限和所有警告臨界值。  
  
```  
EXEC sp_dbmmonitordropalert AdventureWorks2012 ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)  
  
  
