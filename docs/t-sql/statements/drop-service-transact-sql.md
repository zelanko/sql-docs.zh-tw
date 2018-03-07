---
title: "卸除服務 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_SERVICE_TSQL
- DROP SERVICE
dev_langs:
- TSQL
helpviewer_keywords:
- deleting services
- services [Service Broker], removing
- dropping services
- DROP SERVICE statement
- removing services
ms.assetid: 2351bba7-0f2a-4cda-b3b2-6a88b8747c53
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17d968946d57293f147483833e58c1d1a2395b7b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="drop-service-transact-sql"></a>DROP SERVICE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  卸除現有的服務。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP SERVICE service_name  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *服務名稱*  
 要卸除的服務名稱。 您不可指定伺服器、資料庫和結構描述名稱。  
  
## <a name="remarks"></a>備註  
 當有任何交談優先權參考服務時，您將無法卸除此服務。  
  
 卸除服務會從服務使用的佇列中，刪除此服務的所有訊息。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會將錯誤傳送到使用此服務之任何開啟交談的遠端。  
  
## <a name="permissions"></a>Permissions  
 卸除服務的權限預設為服務的擁有者、db_ddladmin 或 db_owner 固定資料庫角色的成員，以及系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會卸除 `//Adventure-Works.com/Expenses` 服務。  
  
```  
DROP SERVICE [//Adventure-Works.com/Expenses] ;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [ALTER BROKER PRIORITY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [ALTER 服務 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
