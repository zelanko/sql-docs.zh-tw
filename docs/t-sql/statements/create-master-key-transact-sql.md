---
title: "建立主要金鑰 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e051e59ebae464942068521a95a1d5b06389304e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-master-key-transact-sql"></a>CREATE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
 密碼 ='*密碼*'  
 這是用以加密資料庫中主要金鑰的密碼。 *密碼*必須符合正在執行的執行個體之電腦的 Windows 密碼原則需求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 *密碼*是選擇性的[!INCLUDE[ssSDS](../../includes/sssds-md.md)]和[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。  
  
## <a name="remarks"></a>備註  
 資料庫主要金鑰是一個用來保護憑證私密金鑰和資料庫中非對稱金鑰的對稱金鑰。 建立資料庫主要金鑰時，系統會利用 AES_256 演算法和使用者提供的密碼來加密主要金鑰。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]，使用 TRIPLE DES 演算法。 若要啟用主要金鑰的自動解密，必須利用服務主要金鑰來加密該金鑰的副本，並將它同時儲存在資料庫和 master 中。 通常，每當主要金鑰變更時，儲存在 master 中的副本便會以無訊息模式更新。 來變更此預設值，請使用 DROP ENCRYPTION BY SERVICE MASTER KEY 選項[ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md)。 未以服務主要金鑰加密主要金鑰必須開啟使用[OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md)陳述式和密碼。  
  
 master 中之 sys.databases 目錄檢視的 is_master_key_encrypted_by_server 資料行會指出是否利用服務主要金鑰來加密資料庫主要金鑰。  
  
 您可以在 sys.symmetric_keys 目錄檢視中，看到有關資料庫主要金鑰的資訊。  

對於 SQL Server 與平行處理資料倉儲，主要金鑰通常受到服務主要金鑰和至少一個密碼。 如果實際移動到不同的伺服器 （記錄傳送，請還原備份等） 的資料庫，資料庫會包含 （除非此加密已明確地移除使用原始伺服器服務主要金鑰所加密的主要金鑰的副本ALTER MASTER KEY DDL)，以及每個 CREATE MASTER KEY 或後續 ALTER MASTER KEY DDL 作業期間所指定的密碼來加密它的複本。 為了進行復原，主要金鑰和加密在移動資料庫之後，使用主要金鑰做為根機碼階層架構中的所有資料，使用者必須使用 OPEN MASTER KEY 陳述式使用其中一種用來保護主要金鑰的密碼還原的主要金鑰備份或還原備份的原始服務主要金鑰的新伺服器上。 

如[!INCLUDE[ssSDS](../../includes/sssds-md.md)]和[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]，不視為密碼保護的安全性機制，以避免資料遺失情況情況下，資料庫可能從某部伺服器移到另一個，因為主要金鑰的服務主要金鑰保護受 Microsoft Azure 平台。 因此，微波金鑰密碼是在選擇性[!INCLUDE[ssSDS](../../includes/sssds-md.md)]和[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。
  
> [!IMPORTANT]  
>  您應該透過備份主要金鑰[備份主要金鑰](../../t-sql/statements/backup-master-key-transact-sql.md)將備份儲存在安全且位於異地的位置。  
  
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
 [sys.symmetric_keys &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [開啟主要金鑰 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  



