---
title: "SETUSER (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
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
- SETUSER_TSQL
- SETUSER
dev_langs:
- TSQL
helpviewer_keywords:
- delegation [SQL Server]
- impersonation [SQL Server]
- SETUSER statement
- user impersonation [SQL Server]
ms.assetid: 7acfac5c-9ad6-4226-b874-7add36c4ea43
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a511e0337201c9b4501b5274fa8270fbebf7da50
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="setuser-transact-sql"></a>SETUSER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  允許的成員**sysadmin**固定伺服器角色或資料庫擁有者可以模擬另一位使用者。  
  
> [!IMPORTANT]  
>  包括 SETUSER 的目的，只是為了與舊版相容。 未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本可能不支援 SETUSER。 我們建議您改用[EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SETUSER [ 'username' [ WITH NORESET ] ]   
```  
  
## <a name="arguments"></a>引數  
 **'** *username* **'**  
 這是在模擬的目前資料庫中之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Windows 使用者名稱。 當*username*未指定，就會重設原始的身分識別的系統管理員或資料庫擁有者模擬使用者。  
  
 WITH NORESET  
 指定後續的 SETUSER 陳述式 (不含指定*username*) 應該不重設的使用者識別為系統管理員或資料庫擁有者。  
  
## <a name="remarks"></a>備註  
 SETUSER 可用的成員所**sysadmin**固定伺服器角色或資料庫擁有者採用以測試其他使用者的權限的另一位使用者的識別。 中的 db_owner 固定資料庫角色的成員資格是不夠的。  
  
 請只搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者使用 SETUSER。 不支援 Windows 使用者使用 SETUSER。 當利用 SETUSER 來假設使用另一位使用者的識別時，被模擬的使用者會擁有進行模擬的使用者所建立的任何物件。 例如，如果資料庫擁有者假設使用者的身分識別**Margaret**並建立名為的資料表**訂單**、**訂單**資料表擁有者是**Margaret**，不是系統管理員。  
  
 SETUSER 會維持有效，直到發出另一個 SETUSER 陳述式，或直到利用 USE 陳述式來變更目前資料庫為止。  
  
> [!NOTE]  
>  如果使用 SETUSER WITH NORESET，資料庫擁有者或系統管理員必須登出，再重新登入，以便重新建立他們自己的權利。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定伺服器角色，或必須是資料庫擁有者。 中的成員資格**db_owner**不足的固定的資料庫角色  
  
## <a name="examples"></a>範例  
 下列範例會顯示資料庫擁有者可以如何採用另一位使用者的識別。 `mary` 使用者建立了稱為 `computer_types` 的資料表。 藉由使用 SETUSER，資料庫擁有者模擬 `mary` 來授與 `joe` 使用者存取 `computer_types` 資料表的權利，然後再重設他們自己的識別。  
  
```  
SETUSER 'mary';  
GO  
GRANT SELECT ON computer_types TO joe;  
GO  
--To revert to the original user  
SETUSER;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  
