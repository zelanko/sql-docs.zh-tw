---
title: sp_control_dbmasterkey_password(轉算-SQL) |微軟文件
ms.custom: ''
ms.date: 04/09/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_control_dbmasterkey_password
- sp_control_dbmasterkey_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_dbmasterkey_password
ms.assetid: 63979a87-42a2-446e-8e43-30481faaf3ca
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 620a174f50d133c4a1dd34ed54c74abb7ee06a71
ms.sourcegitcommit: fbe0ab88fa8d5aa3ea96629f4ccfa4da5caf74f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/10/2020
ms.locfileid: "81012440"
---
# <a name="sp_control_dbmasterkey_password-transact-sql"></a>sp_control_dbmasterkey_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  加入或卸除認證，其中包含開啟資料庫主要金鑰所需的密碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_control_dbmasterkey_password @db_name = 'database_name,  
     @password = 'master_key_password' , @action = { 'add' | 'drop' }  
```  
  
## <a name="arguments"></a>引數  
 @db_name[N'*database_name*'  
 指定這個認證的相關資料庫名稱。 不能是系統資料庫。 *database_name*是**恩瓦爾查爾**。  
  
 @password*N'*密碼*'  
 指定主要金鑰的密碼。 *密碼*是**nvarchar。**  
  
 @action[N'add'  
 指定要將指定資料庫的認證加入至認證存放區中。 認證會包含資料庫主要金鑰的密碼。 傳遞給@action的值是**nvarchar**。  
  
 @action[N'下降'  
 指定要從認證存放區中卸除指定資料庫的認證。 傳遞給@action的值是**nvarchar**。  
  
## <a name="remarks"></a>備註  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要利用資料庫主要金鑰解密或加密金鑰時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會嘗試利用執行個體的服務主要金鑰來解密資料庫主要金鑰。 如果解密失敗，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會從認證存放區中搜尋主要金鑰認證，這些主要金鑰認證具有與它需要其主要金鑰之資料庫相同的家族 GUID。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會嘗試利用每個相符的認證來將資料庫主要金鑰解密，直到解密成功或沒有其他認證為止。  
  
> [!CAUTION]  
>  請勿建立一個不能由 sa 和其他高權限伺服器主體存取之資料庫的主要金鑰認證。 您可以將資料庫設為不能由服務主要金鑰解密它的金鑰階層。 這個選項可作為特定資料庫的深度防衛，該等資料庫所含加密資訊不應該由 sa 或其他高權限伺服器主體存取。 建立這類資料庫的主要金鑰認證會移除這個深度防衛，使 sa 和其他高權限伺服器主體能夠解密資料庫。  
  
 使用sp_control_dbmasterkey_password創建的憑據在[sys.master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md)目錄視圖中可見。 為資料庫主要金鑰建立的認證名稱採用下列格式：`##DBMKEY_<database_family_guid>_<random_password_guid>##`。 密碼會儲存為認證秘密。 就加入至認證存放區的每個密碼而言，sys.credentials 中都有資料列。  
  
 您無法利用 sp_control_dbmasterkey_password 建立下列系統資料庫的認證：master、model、msdb 或 tempdb。  
  
 sp_control_dbmasterkey_password 不確認密碼可以開啟指定資料庫的主要金鑰。  
  
 如果您指定的密碼已儲存在指定資料庫的認證中，sp_control_dbmasterkey_password 會失敗。  
  
> [!NOTE]  
>  來自不同伺服器執行個體的兩個資料庫可以共用相同的家族 GUID。 如果發生這種情況，這兩個資料庫會共用認證存放區中相同的主要金鑰記錄。  
  
 傳遞至 sp_control_dbmasterkey_password 的參數不會出現在追蹤中。  
  
> [!NOTE]  
>  當您使用的認證是之前使用 sp_control_dbmasterkey_password 開啟資料庫主要金鑰所加入的認證時，服務主要金鑰會重新加密資料庫主要金鑰。 如果資料庫處於唯讀模式，重新加密作業將會失敗，而且資料庫主要金鑰會維持未加密的狀態。 之後如果要存取資料庫主要金鑰，您必須使用 OPEN MASTER KEY 陳述式和密碼。 若要避免使用密碼，將資料庫移到唯讀模式之前要先建立認證。  
  
 **潛在的向後相容性問題:** 目前,存儲過程不檢查主密鑰是否存在。 這可允許回溯相容性，但是會顯示警告。 這個行為已被取代。 在將來的版本中,主密鑰必須存在,並且存儲過程中使用的密碼**sp_control_dbmasterkey_password**必須與用於加密資料庫主金鑰的密碼之一的密碼相同。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員**固定伺服器角色的成員身份。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-credential-for-the-adventureworks2012-master-key"></a>A. 建立 AdventureWorks2012 主要金鑰的認證  
 下列範例會建立 `AdventureWorks2012` 資料庫主要金鑰的認證，並將主要金鑰密碼儲存為認證中的秘密。 由於傳送所有所有`sp_control_dbmasterkey_password`參數 必須為資料型**態 nvarchar,** 因此文字字串會將隨`N`強制轉換運算子 。  
  
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
 [安全儲存過程&#40;處理-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [系統儲存過程&#40;處理-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [系統認證&#40;交易-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [認證 &#40;資料庫引擎&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)  
  
  
