---
title: "卸除登入 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP LOGIN
- DROP_LOGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting login accounts
- logins [SQL Server], removing
- DROP LOGIN statement
- removing login accounts
- dropping login accounts
ms.assetid: acb5c3dc-7aa2-49f6-9330-573227ba9b1a
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c8c13d7800893b860b1bcaf3f631f01f190a2715
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-login-transact-sql"></a>DROP LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入帳戶。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DROP LOGIN login_name  
```  
  
## <a name="arguments"></a>引數  
 *login_name*  
 指定要卸除之登入的名稱。  
  
## <a name="remarks"></a>備註  
 已登入的登入無法卸除。 擁有安全性實體、伺服器層級物件或 SQL Server Agent 作業的登入也無法卸除。  
  
 您可以卸除資料庫使用者對應的登入；然而，這會建立被遺棄的使用者。 如需詳細資訊，請參閱 [孤立的使用者疑難排解 &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)。  
  
 在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]、 驗證連線所需的登入資料和伺服器層級防火牆規則中每個資料庫會暫時快取。 此快取會定期重新整理。 若要強制驗證快取重新整理，並請確定資料庫有登入資料表的最新版本，執行[DBCC FLUSHAUTHCACHE &#40;TRANSACT-SQL &#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 ALTER ANY LOGIN 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-dropping-a-login"></a>A. 卸除登入  
 下列範例會卸除登入 `WilliJo`。  
  
```  
DROP LOGIN WilliJo;  
GO 
```  
 
  
## <a name="see-also"></a>另請參閱  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  


