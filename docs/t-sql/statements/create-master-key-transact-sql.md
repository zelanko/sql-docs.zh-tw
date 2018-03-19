---
title: CREATE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
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
- CREATE_MASTER_KEY_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- CREATE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], Database Master Key
- database master key [SQL Server]
- CREATE MASTER KEY statement
- cryptography [SQL Server], Database Master Key
- database master key [SQL Server], creating
ms.assetid: 1710a305-1a4f-48ec-836c-11ffd0356d76
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aaec4d28dc95d792faa6406ef68df50167d0f091
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="create-master-key-transact-sql"></a>CREATE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  建立資料庫主要金鑰。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Parallel Data Warehouse  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password'  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE MASTER KEY [ ENCRYPTION BY PASSWORD ='password' ]
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 PASSWORD ='*password*'  
 這是用以加密資料庫中主要金鑰的密碼。 *password* 必須符合執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之電腦的 Windows 密碼原則需求。 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 和 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 中，*password* 為選擇性。  
  
## <a name="remarks"></a>Remarks  
 資料庫主要金鑰是一個用來保護憑證私密金鑰和資料庫中非對稱金鑰的對稱金鑰。 建立資料庫主要金鑰時，系統會利用 AES_256 演算法和使用者提供的密碼來加密主要金鑰。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]，使用 TRIPLE DES 演算法。 若要啟用主要金鑰的自動解密，必須利用服務主要金鑰來加密該金鑰的副本，並將它同時儲存在資料庫和 master 中。 通常，每當主要金鑰變更時，儲存在 master 中的副本便會以無訊息模式更新。 您可以使用 [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md) 的 DROP ENCRYPTION BY SERVICE MASTER KEY 選項來變更這個預設值。 如果主要金鑰未以服務主要金鑰來加密，則必須使用 [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) 陳述式和密碼來開啟。  
  
 master 中之 sys.databases 目錄檢視的 is_master_key_encrypted_by_server 資料行會指出是否利用服務主要金鑰來加密資料庫主要金鑰。  
  
 您可以在 sys.symmetric_keys 目錄檢視中，看到有關資料庫主要金鑰的資訊。  

針對 SQL Server 與平行處理資料倉儲，主要金鑰通常由服務主要金鑰和至少一個密碼來保護。 如果資料庫要實際移動到不同的伺服器 (記錄傳送、還原備份等)，資料庫會包含以原始伺服器服務主要金鑰所加密的主要金鑰複本 (除非已使用 ALTER MASTER KEY DDL 明確移除此加密)，以及在 CREATE MASTER KEY 或後續 ALTER MASTER KEY DDL 作業期間由每個指定密碼加密的複本。 若要在移動資料庫之後復原主要金鑰與所有資料 (已使用主要金鑰作為金鑰階層中的根加密)，使用者必須使用 OPEN MASTER KEY 陳述式與其中一個用來保護主要金鑰的密碼來還原主要金鑰備份，或在新伺服器上還原原始服務主要金鑰備份。 

若是 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 和 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]，在資料庫可以從某部伺服器移到另一部伺服器的情況下，密碼保護並非避免資料遺失的安全機制，因為主要金鑰上的服務主要金鑰保護是由 Microsoft Azure 平台來管理。 因此，主要金鑰密碼在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 和 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 中為選擇性的。
  
> [!IMPORTANT]  
>  您應該使用 [BACKUP MASTER KEY](../../t-sql/statements/backup-master-key-transact-sql.md) 來備份主要金鑰，然後將該備份儲存在安全的離站位置。  
  
 服務主要金鑰和資料庫主要金鑰，皆使用 AES-256 演算法加以保護。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會建立目前資料庫的資料庫主要金鑰。 這個金鑰是利用密碼 `23987hxJ#KL95234nl0zBe` 來加密的。  
  
```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
GO  
```  

  
## <a name="see-also"></a>另請參閱  
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


