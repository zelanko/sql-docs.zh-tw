---
title: ALTER MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER MASTER KEY
- ALTER_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- ALTER MASTER KEY statement
- decryption [SQL Server], Database Master Key
- FORCE option
- encryption [SQL Server], Database Master Key
- database master key [SQL Server], modifying
- cryptography [SQL Server], Database Master Key
- modifying Database Master Key
- service master key [SQL Server], modifying
- DROP ENCRYPTION BY SERVICE MASTER KEY phrase
ms.assetid: 8ac501c3-4280-4d5b-b58a-1524fa715b50
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0e664b594017b7131553869d1696708eae3b52b0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-master-key-transact-sql"></a>ALTER MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  變更資料庫主要金鑰的屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD = 'password'  
  
<encryption_option> ::=  
    ADD ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
    |   
    DROP ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
```  
```  
-- Syntax for Azure SQL Database
-- Note: DROP ENCRYPTION BY SERVICE MASTER KEY is not supported on Azure SQL Database.
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD = 'password'  
  
<encryption_option> ::=  
    ADD ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
    |   
    DROP ENCRYPTION BY { PASSWORD = 'password' }  
```  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD ='password'<encryption_option> ::=  
    ADD ENCRYPTION BY SERVICE MASTER KEY   
    |   
    DROP ENCRYPTION BY SERVICE MASTER KEY  
```  
  
## <a name="arguments"></a>引數  
 PASSWORD ='*password*'  
 指定用於加密或解密資料庫主要金鑰的密碼。 *password* 必須符合執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之電腦的 Windows 密碼原則需求。  
  
## <a name="remarks"></a>Remarks  
 REGENERATE 選項會重新建立資料庫主要金鑰和它保護的所有金鑰。 會先利用舊的主要金鑰解密這些金鑰，然後利用新的主要金鑰加密它們。 除非已危害到主要金鑰，否則，這項需要大量資源的作業應該安排在低需求時進行。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 是使用 AES 加密演算法來保護服務主要金鑰 (SMK) 及資料庫主要金鑰 (DMK)。 與早期版本中使用的 3DES 相比，AES 是一種較新的加密演算法。 將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體升級至 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 之後，應該會重新產生 SMK 和 DMK，以將主要金鑰升級至 AES。 如需重新產生 SMK 的詳細資訊，請參閱 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)。  
  
 當使用 FORCE 選項時，即使主要金鑰無法使用或伺服器無法解密所有加密私密金鑰，仍會繼續重新產生金鑰。 如果無法開啟主要金鑰，請使用 [RESTORE MASTER KEY](../../t-sql/statements/restore-master-key-transact-sql.md) 陳述式，從備份還原主要金鑰。 請只在主要金鑰無法擷取或解密失敗時才使用 FORCE 選項。 只由無法擷取的金鑰加密的資訊會遺失。  
  
 DROP ENCRYPTION BY SERVICE MASTER KEY 選項會移除服務主要金鑰對資料庫主要金鑰所執行的加密。  
  
 ADD ENCRYPTION BY SERVICE MASTER KEY 會造成利用服務主要金鑰來加密主要金鑰的副本，並將該副本同時儲存在目前資料庫和 master 中。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 CONTROL 權限。 如果已利用密碼加密資料庫主要金鑰，則還需要知道該密碼。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `AdventureWorks` 的新資料庫主要金鑰，並在加密階層中重新加密在它下方的金鑰。  
  
```  
USE AdventureWorks2012;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會建立 `AdventureWorksPDW2012` 的新資料庫主要金鑰，並在加密階層中重新加密其下方的金鑰。  
  
```  
USE master;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  

