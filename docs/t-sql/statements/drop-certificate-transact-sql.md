---
title: "卸除憑證 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
- DROP CERTIFICATE
- DROP_CERTIFICATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], removing
- removing certificates
- dropping certificates
- DROP CERTIFICATE statement
- deleting certificates
ms.assetid: 5704aa04-68a3-4b29-b62b-8868af487817
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f68e801dfbc073e1ecccbf347589a891e2a3d032
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-certificate-transact-sql"></a>DROP CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  從資料庫中移除憑證。  
  
> [!IMPORTANT]  
>  凡是用於資料庫加密的憑證都應該保留備份，即便是資料庫已經不再啟用加密。 就算資料庫已不再加密，交易記錄的某些部分可能仍受到保護，因而有些作業截至資料庫執行完整備份為止或許都需要此憑證。 您也必須有此憑證，才能夠從資料庫加密當時所建立的備份還原。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DROP CERTIFICATE certificate_name  
```  
  
## <a name="arguments"></a>引數  
 *certificate_name*  
 這是資料庫中憑證的唯一識別名稱。  
  
## <a name="remarks"></a>備註  
 憑證只有在沒有實體與其關聯時，才可以卸除。  
  
## <a name="permissions"></a>Permissions  
 需要憑證的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從 `Shipping04` 資料庫卸除憑證 `AdventureWorks`。  
  
```  
USE AdventureWorks2012;  
DROP CERTIFICATE Shipping04;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會卸除憑證`Shipping04`。  
  
```  
USE master;  
DROP CERTIFICATE Shipping04;  
```  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


