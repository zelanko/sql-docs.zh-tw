---
title: SETUSER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 66830b3000d749ab17a5800c3450c5880c5d1aba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076439"
---
# <a name="setuser-transact-sql"></a>SETUSER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  允許 **sysadmin** 固定伺服器角色的成員或資料庫的擁有者，模擬其他使用者。  
  
> [!IMPORTANT]  
>  包括 SETUSER 的目的，只是為了與舊版相容。 未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本可能不支援 SETUSER。 我們建議您改用 [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SETUSER [ 'username' [ WITH NORESET ] ]   
```  
  
## <a name="arguments"></a>引數  
 **'** *username* **'**  
 這是在模擬的目前資料庫中之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Windows 使用者名稱。 當未指定 *username* 時，會重設摸擬使用者的系統管理員或資料庫擁有者的原始識別。  
  
 WITH NORESET  
 指定後續的 SETUSER 陳述式 (不含指定的 *username*) 不應將使用者識別重設為系統管理員或資料庫擁有者。  
  
## <a name="remarks"></a>Remarks  
 **sysadmin** 固定伺服器角色的成員或資料庫的擁有者，可以使用 SETUSER 來採用其他使用者的識別，以測試另一位使用者的權限。 db_owner 固定資料庫角色中的成員資格並不夠。  
  
 請只搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者使用 SETUSER。 不支援 Windows 使用者使用 SETUSER。 當利用 SETUSER 來假設使用另一位使用者的識別時，被模擬的使用者會擁有進行模擬的使用者所建立的任何物件。 例如，假設資料庫擁有者使用 **Margaret** 使用者的識別，並建立稱為 **orders** 的資料表，則 **orders** 資料表的擁有者即為 **Margaret**，而不是系統管理員。  
  
 SETUSER 會維持有效，直到發出另一個 SETUSER 陳述式，或直到利用 USE 陳述式來變更目前資料庫為止。  
  
> [!NOTE]  
>  如果使用 SETUSER WITH NORESET，資料庫擁有者或系統管理員必須登出，再重新登入，以便重新建立他們自己的權利。  
  
## <a name="permissions"></a>權限  
 需要 **sysadmin** 固定伺服器角色的成員資格，或必須為資料庫的擁有者。 **db_owner** 固定資料庫角色中的成員資格不足  
  
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
  
## <a name="see-also"></a>另請參閱  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  
