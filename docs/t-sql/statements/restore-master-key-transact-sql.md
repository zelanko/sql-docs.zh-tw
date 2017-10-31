---
title: "還原主要金鑰 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE_MASTER_KEY_TSQL
- RESTORE MASTER KEY
- LOAD_MASTER_KEY_TSQL
- LOAD MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- database master key [SQL Server], importing
- encryption [SQL Server], Database Master Key
- copying Database Master Keys
- importing Database Master Keys
- cryptography [SQL Server], Database Master Key
- transferring Database Master Keys
- RESTORE MASTER KEY statement
ms.assetid: 70ceb951-31a2-4fc4-a0c1-e6c18eeb3ae7
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 941c6bd886615588ca74bf92de6665e25db224a0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="restore-master-key-transact-sql"></a>RESTORE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從備份檔案匯入資料庫主要金鑰。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
RESTORE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password'  
    ENCRYPTION BY PASSWORD = 'password'  
    [ FORCE ]  
```  
  
## <a name="arguments"></a>引數  
 檔案 ='*path_to_file*'  
 指定預存資料庫主要金鑰的完整路徑，包括檔案名稱。 *path_to_file*可以是本機路徑或通往網路位置的 UNC 路徑。  
  
 DECRYPTION BY PASSWORD ='*密碼*'  
 指定解密要從檔案匯入之資料庫主要金鑰時所需的密碼。  
  
 ENCRYPTION BY PASSWORD ='*密碼*'  
 指定資料庫主要金鑰已載入資料庫中之後用來加密該金鑰的密碼。  
  
 FORCE  
 即使目前資料庫主要金鑰未開啟，或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法解密某些以此金鑰加密的私密金鑰時，指定 RESTORE 處理序仍應繼續執行。  
  
## <a name="remarks"></a>備註  
 當主要金鑰還原時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會解密所有利用目前作用中主要金鑰加密的金鑰，然後利用還原的主要金鑰加密這些金鑰。 這項需要大量資源的作業應該安排在低需求時進行。 如果目前資料庫主要金鑰未開啟或無法開啟，或者，如果利用該金鑰加密的任何金鑰無法解密，還原作業便會失敗。  
  
 請只在主要金鑰無法擷取或解密失敗時才使用 FORCE 選項。 只由無法擷取的金鑰加密的資訊會遺失。  
  
 如果先前是由服務主要金鑰加密主要金鑰，則還原的主要金鑰也會由服務主要金鑰來加密。  
  
 如果目前資料庫中沒有主要金鑰，RESTORE MASTER KEY 會建立主要金鑰。 不會自動利用服務主要金鑰來加密新的主要金鑰。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會還原 `AdventureWorks2012` 資料庫的資料庫主要金鑰。  
  
```  
USE AdventureWorks2012;  
RESTORE MASTER KEY   
    FROM FILE = 'c:\backups\keys\AdventureWorks2012_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
    ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

