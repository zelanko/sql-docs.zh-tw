---
title: "OPEN MASTER KEY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- OPEN MASTER KEY DECRYPTION BY PASSWORD
- OPEN_MASTER_KEY_DECRYPTION_BY_PASSWORD_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- OPEN_MASTER_KEY_TSQL
- MASTER KEY DECRYPTION
- OPEN MASTER KEY
- MASTER_KEY_DECRYPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- opening Database Master Keys
- encryption [SQL Server], Database Master Key
- cryptography [SQL Server], Database Master Key
- master key decryption
- OPEN MASTER KEY statement
- database master key [SQL Server], opening
ms.assetid: 1674753e-ca1e-4913-9ba4-b442e7106121
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ef9e8331c891a6087e55b4eb70b19dda4057bf2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="open-master-key-transact-sql"></a>OPEN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  開啟目前資料庫的資料庫主要金鑰。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>引數  
 '*密碼*'  
 用來加密資料庫主要金鑰的密碼。  
  
## <a name="remarks"></a>備註  
 如果利用服務主要金鑰來加密資料庫主要金鑰，則在解密或加密需要它時，會自動加以開啟。 在此情況下，不需要使用**OPEN MASTER KEY**陳述式。  
  
 當資料庫第一次連接或還原到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體時，資料庫主要金鑰複本 (由服務主要金鑰加密) 尚未儲存在伺服器中。 您必須利用 **OPEN MASTER KEY** 陳述式來解密資料庫主要金鑰 (DMK)。 DMK 解密之後，您便可以選擇利用 **ALTER MASTER KEY REGENERATE** 陳述式來提供服務主要金鑰 (SMK) 所加密的 DMK 複本給伺服器，以在未來啟用自動解密。 當資料庫從舊版升級時，應該會重新產生 DMK 以使用較新的 AES 演算法。 如需重新產生 DMK 的詳細資訊，請參閱 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)。 重新產生 DMK 金鑰以升級至 AES 所需的時間是取決於 DMK 所保護的物件數目而定。 重新產生 DMK 金鑰以升級至 AES 只需執行一次，且不會影響金鑰循環策略中後續的重新產生。  
  
 您可以設定 DROP ENCRYPTION BY SERVICE MASTER KEY 選項來使用 ALTER MASTER KEY 陳述式，以從自動金鑰管理中排除特定資料庫的資料庫主要金鑰。 之後，您必須利用密碼來明確開啟資料庫主要金鑰。  
  
 如果回復明確開啟資料庫主要金鑰的交易，金鑰會維持開啟狀態。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會開啟 `AdventureWorks2012` 資料庫已利用密碼來加密的資料庫主要金鑰。  
  
```  
USE AdventureWorks2012;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會開啟資料庫主要，其中已利用密碼加密。  
  
```  
USE master;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO  
CLOSE MASTER KEY;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [還原 MASTER KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


