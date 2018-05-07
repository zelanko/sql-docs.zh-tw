---
title: sp_control_dbmasterkey_password (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_control_dbmasterkey_password
- sp_control_dbmasterkey_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_dbmasterkey_password
ms.assetid: 63979a87-42a2-446e-8e43-30481faaf3ca
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a9894a10965affbd65406276445f6c84f05ce76e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spcontroldbmasterkeypassword-transact-sql"></a>sp_control_dbmasterkey_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  加入或卸除認證，其中包含開啟資料庫主要金鑰所需的密碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_control_dbmasterkey_password @db_name = 'database_name,  
     @password = 'master_key_password' , @action = { 'add' | 'drop' }  
```  
  
## <a name="arguments"></a>引數  
 @db_name= N'*database_name*'  
 指定這個認證的相關資料庫名稱。 不能是系統資料庫。 *database_name*是**nvarchar**。  
  
 @password= N'*密碼*'  
 指定主要金鑰的密碼。 *密碼*是**nvarchar**。  
  
 @action= N'add'  
 指定要將指定資料庫的認證加入至認證存放區中。 認證會包含資料庫主要金鑰的密碼。 傳遞給的值@action是**nvarchar**。  
  
 @action= N'drop'  
 指定要從認證存放區中卸除指定資料庫的認證。 傳遞給的值@action是**nvarchar**。  
  
## <a name="remarks"></a>備註  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要利用資料庫主要金鑰解密或加密金鑰時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會嘗試利用執行個體的服務主要金鑰來解密資料庫主要金鑰。 如果解密失敗，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會從認證存放區中搜尋主要金鑰認證，這些主要金鑰認證具有與它需要其主要金鑰之資料庫相同的家族 GUID。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會嘗試利用每個相符的認證來將資料庫主要金鑰解密，直到解密成功或沒有其他認證為止。  
  
> [!CAUTION]  
>  請勿建立一個不能由 sa 和其他高權限伺服器主體存取之資料庫的主要金鑰認證。 您可以將資料庫設為不能由服務主要金鑰解密它的金鑰階層。 這個選項可作為特定資料庫的深度防衛，該等資料庫所含加密資訊不應該由 sa 或其他高權限伺服器主體存取。 建立這類資料庫的主要金鑰認證會移除這個深度防衛，使 sa 和其他高權限伺服器主體能夠解密資料庫。  
  
 利用 sp_control_dbmasterkey_password 建立認證會顯示在[sys.master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md)目錄檢視。 為資料庫主要金鑰建立的認證名稱採用下列格式：`##DBMKEY_<database_family_guid>_<random_password_guid>##`。 密碼會儲存為認證秘密。 就加入至認證存放區的每個密碼而言，sys.credentials 中都有資料列。  
  
 您無法利用 sp_control_dbmasterkey_password 建立下列系統資料庫的認證：master、model、msdb 或 tempdb。  
  
 sp_control_dbmasterkey_password 不確認密碼可以開啟指定資料庫的主要金鑰。  
  
 如果您指定的密碼已儲存在指定資料庫的認證中，sp_control_dbmasterkey_password 會失敗。  
  
> [!NOTE]  
>  來自不同伺服器執行個體的兩個資料庫可以共用相同的家族 GUID。 如果發生這種情況，這兩個資料庫會共用認證存放區中相同的主要金鑰記錄。  
  
 傳遞至 sp_control_dbmasterkey_password 的參數不會出現在追蹤中。  
  
> [!NOTE]  
>  當您使用的認證是之前使用 sp_control_dbmasterkey_password 開啟資料庫主要金鑰所加入的認證時，服務主要金鑰會重新加密資料庫主要金鑰。 如果資料庫處於唯讀模式，重新加密作業將會失敗，而且資料庫主要金鑰會維持未加密的狀態。 之後如果要存取資料庫主要金鑰，您必須使用 OPEN MASTER KEY 陳述式和密碼。 若要避免使用密碼，將資料庫移到唯讀模式之前要先建立認證。  
  
 **可能的回溯相容性問題：**目前預存程序不會檢查主要金鑰是否存在。 這可允許回溯相容性，但是會顯示警告。 這個行為已被取代。 在未來的版本，主要金鑰必須存在，預存程序中使用的密碼**sp_control_dbmasterkey_password**必須是相同的密碼做為其中一個用來加密資料庫主要金鑰的密碼。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-credential-for-the-adventureworks2012-master-key"></a>A. 建立 AdventureWorks2012 主要金鑰的認證  
 下列範例會建立 `AdventureWorks2012` 資料庫主要金鑰的認證，並將主要金鑰密碼儲存為認證中的秘密。 因為所有的參數傳遞給`sp_control_dbmasterkey_password`的資料類型必須是**nvarchar**，文字字串會轉換轉型運算子`N`。  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'add';  
GO  
```  
  
### <a name="b-dropping-a-credential-for-a-database-master-key"></a>B. 卸除資料庫主要金鑰的認證  
 下列範例會移除範例 A 中建立的認證。請注意，所有參數都需要，包括密碼。  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'drop';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [設定加密鏡像資料庫](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [認證 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)  
  
  
