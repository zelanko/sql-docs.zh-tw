---
title: LOGINPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BadPasswordCount_TSQL
- BadPasswordTime_TSQL
- IsLockedIsMustChange
- PasswordLastSetTime
- LOGINPROPERTY_TSQL
- LockoutTime
- BadPasswordCount
- PasswordHash
- HistoryLengthIsExpired
- LockoutTime_TSQL
- PasswordHash_TSQL
- HistoryLengthIsExpired_TSQL
- PasswordLastSetTime_TSQL
- BadPasswordTime
- IsLockedIsMustChange_TSQL
- LOGINPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- default database
- LOGINPROPERTY function
ms.assetid: b34df777-79b0-49a5-88db-b99998479a5d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e081af76034b467a84eb6dbf81ab3b884a4440fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65949141"
---
# <a name="loginproperty-transact-sql"></a>LOGINPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關登入原則設定的詳細資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
LOGINPROPERTY ( 'login_name' , 'property_name' )  
```  
  
## <a name="arguments"></a>引數  
 *login_name*  
 這是要傳回登入屬性狀態之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的名稱。  
  
 *propertyname*  
 這是包含為登入傳回之屬性資訊的運算式。 *propertyname* 可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**BadPasswordCount**|傳回連續使用錯誤密碼嘗試登入的次數。|  
|**BadPasswordTime**|傳回上一次使用錯誤密碼嘗試登入的時間。|  
|**DaysUntilExpiration**|傳回密碼到期之前的剩餘天數。|  
|**DefaultDatabase**|傳回儲存在中繼資料中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入預設資料庫 (在未指定任何資料庫的情況下，則為 **master**)。 針對非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佈建的使用者傳回 NULL (例如 Windows 驗證的使用者)。|  
|**DefaultLanguage**|傳回登入預設語言 (儲存於中繼資料內)。 針對非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佈建的使用者傳回 NULL，例如 Windows 驗證的使用者。|  
|**HistoryLength**|利用密碼原則強制執行機制，傳回追蹤登入的密碼數目。 如果密碼原則未強制執行，則為 0。 繼續密碼原則強制執行從 1 重新啟動。|  
|**IsExpired**|指出登入是否已過期。|  
|**IsLocked**|指出登入是否已鎖定。|  
|**IsMustChange**|指出登入是否必須在下次連接時變更其密碼。|  
|**LockoutTime**|傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入因為超過允許的嘗試登入失敗次數而遭鎖定的日期。|  
|**PasswordHash**|傳回密碼雜湊。|  
|**PasswordLastSetTime**|傳回設定目前密碼的日期。|  
|**PasswordHashAlgorithm**|傳回用來雜湊密碼的演算法。|  
  
## <a name="returns"></a>傳回值  
 資料類型相依於要求的值。  
  
 **IsLocked**、**IsExpired** 及 **IsMustChange** 的類型為 **int**。  
  
-   1 代表登入處於指定的狀態。  
  
-   0 代表登入並未處於指定的狀態。  
  
 **BadPasswordCount** 及 **HistoryLength** 的類型為 **int**。  
  
 **BadPasswordTime**、**LockoutTime**、**PasswordLastSetTime** 的類型為 **datetime**。  
  
 **PasswordHash** 的類型為 **varbinary**。  
  
 NULL 代表登入不是有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 **DaysUntilExpiration** 的類型為 **int**。  
  
-   如果登入已過期或是將會在查詢的日期到期，則為 0。  
  
-   如果 Windows 中的本機安全性原則永遠都不會讓密碼過期，則為 -1。  
  
-   如果登入的 CHECK_POLICY 或 CHECK_EXPIRATION 為 OFF，或是作業系統不支援此密碼原則，則為 NULL。  
  
 **PasswordHashAlgorithm** 的類型為 int。  
  
-   如果是 SQL7.0 雜湊，則為 0  
  
-   如果是 SHA-1 雜湊，則為 1  
  
-   如果是 SHA-2 雜湊，則為 2  
  
-   如果登入不是有效的 SQL Server 登入，則為 NULL  
  
## <a name="remarks"></a>Remarks  
 這個內建函數會傳回有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入之密碼原則設定的資訊。 屬性的名稱不區分大小寫，所以 **BadPasswordCount** 和 **badpasswordcount** 之類的屬性名稱是相等的。 **PasswordHash、PasswordHashAlgorithm** 和 **PasswordLastSetTime** 屬性值可用於所有受支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定，但其他屬性則只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 上執行而且同時啟用 CHECK_POLICY 和 CHECK_EXPIRATION 時才可使用。 如需詳細資訊，請參閱＜ [Password Policy](../../relational-databases/security/password-policy.md)＞。  
  
## <a name="permissions"></a>權限  
 需要登入的 VIEW 權限。 在要求密碼雜湊時，也需要 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-checking-whether-a-login-must-change-its-password"></a>A. 檢查登入是否必須變更其密碼  
 下列範例會檢查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `John3` 是否必須在下次連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時變更其密碼。  
  
```  
SELECT LOGINPROPERTY('John3', 'IsMustChange');  
GO  
```  
  
### <a name="b-checking-whether-a-login-is-locked-out"></a>B. 檢查登入是否已經鎖定  
 下列範例會檢查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `John3` 是否已鎖定。  
  
```  
SELECT LOGINPROPERTY('John3', 'IsLocked');  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
  
