---
title: "sp_testlinkedserver (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_testlinkedserver
- sp_testlinkedserver_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_testlinkedserver
ms.assetid: e63ca7d4-47d6-455e-9aac-421f9683dadc
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f3b237d7d48547fec3cad0c1dc412a24a54d4487
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sptestlinkedserver-transact-sql"></a>sp_testlinkedserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  測試與連結伺服器的連接。 如果測試失敗，此程序會引發例外狀況，並顯示失敗的原因。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_testlinkedserver [ @servername ] = servername  
```  
  
## <a name="arguments"></a>引數  
 [  **@servername =** ]*servername*  
 這是連結伺服器的名稱。 *servername*是**sysname**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 沒有檢查任何權限；不過，呼叫端必須具備適當的登入對應才行。  
  
## <a name="examples"></a>範例  
 下列範例會建立名為 `SEATTLESales` 的連結伺服器，然後測試連接。  
  
```  
USE master;  
GO  
EXEC sp_addlinkedserver   
    'SEATTLESales',  
    N'SQL Server';  
GO  
sp_testlinkedserver SEATTLESales;  
GO  
```  
  
## <a name="see-also"></a>請參閱  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)  
  
  
