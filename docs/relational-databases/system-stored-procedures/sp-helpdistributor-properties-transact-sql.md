---
title: sp_helpdistributor_properties （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributor_properties_TSQL
- sp_helpdistributor_properties
helpviewer_keywords:
- sp_helpdistributor_properties
ms.assetid: ee267724-3244-49eb-84c9-f38dbefdd639
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: eca0c3f3c03438c9bcc6a715bf06b4aa58f8690a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733239"
---
# <a name="sp_helpdistributor_properties-transact-sql"></a>sp_helpdistributor_properties (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  傳回散發者屬性。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdistributor_properties   
```  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**heartbeat_interval**|**int**|在未記錄進度訊息的情況下，代理程式所能執行的最大分鐘數。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpdistributor_properties**用於所有類型的複寫。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員、散發資料庫上之**db_owner**或**replmonitor**固定資料庫角色的成員，以及使用此散發者之發行集的發行集存取清單（PAL）中的使用者，才能夠執行**sp_helpdistributor_properties**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_changedistributor_property &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)  
  
  
