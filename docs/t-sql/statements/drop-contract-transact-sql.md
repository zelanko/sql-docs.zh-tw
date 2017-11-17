---
title: "卸除合約 (TRANSACT-SQL) |Microsoft 文件"
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
- DROP_CONTRACT_TSQL
- DROP CONTRACT
dev_langs:
- TSQL
helpviewer_keywords:
- dropping contracts
- removing contracts
- deleting contracts
- contracts [Service Broker], dropping
- DROP CONTRACT statement
ms.assetid: fdd0f81e-3c22-4cdf-9416-b4977a6ac3b6
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 58c76223cf592bc90b4c9cb831f93af943e59154
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-contract-transact-sql"></a>DROP CONTRACT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從資料庫中卸除現有的合約。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP CONTRACT contract_name   
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *contract_name*  
 要卸除的合約名稱。 您不可指定伺服器、資料庫和結構描述名稱。  
  
## <a name="remarks"></a>備註  
 如果有任何服務或交談優先權參考合約，您便不能卸除這份合約。  
  
 當您卸除合約時，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 會結束使用這份合約的任何現有交談，且會出現一則錯誤。  
  
## <a name="permissions"></a>Permissions  
 卸除合約的權限預設為此合約的擁有者、db_ddladmin 或 db_owner 固定資料庫角色的成員，以及系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會從資料庫中移除 `//Adventure-Works.com/Expenses/ExpenseSubmission` 合約。  
  
```  
DROP CONTRACT   
    [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER BROKER PRIORITY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [ALTER 服務 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [建立合約 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [卸除服務 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

