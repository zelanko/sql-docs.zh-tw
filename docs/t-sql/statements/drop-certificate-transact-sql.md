---
title: DROP CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/18/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d84618ef3e5afe74d896899756991d2c0fd40fd1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47750366"
---
# <a name="drop-certificate-transact-sql"></a>DROP CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

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
  
## <a name="remarks"></a>Remarks  
 憑證只有在沒有實體與其關聯時，才可以卸除。  
  
## <a name="permissions"></a>[權限]  
 需要憑證的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從 `Shipping04` 資料庫卸除憑證 `AdventureWorks`。  
  
```  
USE AdventureWorks2012;  
DROP CERTIFICATE Shipping04;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會卸除憑證 `Shipping04`。  
  
```
USE master;  
DROP CERTIFICATE Shipping04;  
```  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
