---
title: PWDCOMPARE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PWDCOMPARE
- PWDCOMPARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sa account
- passwords [SQL Server], blank
- PWDCOMPARE function [Transact-SQL]
ms.assetid: 5f84ff9e-c1ec-46aa-8501-50f854ebcc3a
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ad1e978fd88943aef2f6e2b0bed4bf98f1a96ce0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33056925"
---
# <a name="pwdcompare-transact-sql"></a>PWDCOMPARE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  雜湊密碼並將該雜湊與現有密碼的雜湊相比較。 PWDCOMPARE 可用於搜尋空白的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入密碼或一般弱式密碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
PWDCOMPARE ( 'clear_text_password'  
   , password_hash   
   [ , version ] )  
```  
  
## <a name="arguments"></a>引數  
 **'** *clear_text_password* **'**  
 這是未加密的密碼。 *clear_text_password* is **sysname** (**nvarchar(128)**)。  
  
 *password_hash*  
 這是密碼的加密雜湊。 *password_hash* 為 **varbinary(128)**。  
  
 *version*  
 如果 *password_hash* 代表的登入值早於已經移轉到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本，但從未轉換為 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 系統的 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]，則是可以設定為 1 的已淘汰參數。 *version* 為 **int**。  
  
> [!CAUTION]  
>  提供這個參數是為了回溯相容性，因為密碼雜湊 BLOB 現在包含自己的版本說明，所以會忽略它。 [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
 若 *clear_text_password* 的雜湊符合 *password_hash* 參數，則傳回 1；否則傳回 0。  
  
## <a name="remarks"></a>Remarks  
 PWDCOMPARE 函數並不會對密碼雜湊強度造成威脅，因為可以使用當做第一個參數提供的密碼嘗試登入來執行相同的測試。  
  
 **PWDCOMPARE** 無法與自主資料庫使用者的密碼搭配使用。 沒有任何自主資料庫對等項目。  
  
## <a name="permissions"></a>Permissions  
 PWDENCRYPT 可以公開使用。  
  
 若要檢查 sys.sql_logins 的 password_hash 資料行，需要有 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-identifying-logins-that-have-no-passwords"></a>A. 識別沒有密碼的登入  
 下列範例會識別沒有密碼的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
```  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('', password_hash) = 1 ;  
```  
  
### <a name="b-searching-for-common-passwords"></a>B. 搜尋一般密碼  
 若要搜尋您要識別與變更的一般密碼，請將密碼指定為第一個參數。 例如，執行下列陳述式來搜尋指定為 `password` 的密碼。  
  
```  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('password', password_hash) = 1 ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [PWDENCRYPT &#40;Transact-SQL&#41;](../../t-sql/functions/pwdencrypt-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
