---
title: "DROP ENDPOINT (TRANSACT-SQL) |Microsoft 文件"
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
- DROP_ENDPOINT_TSQL
- DROP ENDPOINT
dev_langs:
- TSQL
helpviewer_keywords:
- removing endpoints
- endpoints [SQL Server], removing
- deleting endpoints
- DROP ENDPOINT statement
- dropping endpoints
ms.assetid: 6aca7412-66a5-4fa4-86b2-061512ff2080
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c823724dbd2f273a161b103b44eb50a77d5f4462
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-endpoint-transact-sql"></a>DROP ENDPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  卸除現有的端點。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP ENDPOINT endPointName  
```  
  
## <a name="arguments"></a>引數  
 *端點名稱*  
 這是要移除的端點名稱。  
  
## <a name="remarks"></a>備註  
 ENDPOINT DDL 陳述式不能在使用者交易內執行。  
  
## <a name="permissions"></a>Permissions  
 使用者必須是成員**sysadmin**固定伺服器角色、 端點的擁有者或被授與端點上的 [控制] 權限。  
  
## <a name="examples"></a>範例  
 下列範例會移除先前建立稱為 `sql_endpoint` 的端點。  
  
```  
DROP ENDPOINT sql_endpoint;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

