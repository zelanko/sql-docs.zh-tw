---
title: SIGNBYCERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SIGNBYCERT
- SIGNBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- text signing [SQL Server]
- encryption [SQL Server], certificates
- certificates [SQL Server], text signing
- SignByCert function
- signing text [SQL Server]
- SIGNBYCERT function
- cryptography [SQL Server], certificates
ms.assetid: b4c6bced-4473-4bae-85b9-56deced495f9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd5940957c3a75555db9032097a99f73639f89bb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="signbycert-transact-sql"></a>SIGNBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  以憑證簽署文字並傳回簽章。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SignByCert ( certificate_ID , @cleartext [ , 'password' ] )  
```  
  
## <a name="arguments"></a>引數  
 *certificate_ID*  
 為目前資料庫中憑證的識別碼。 *certificate_ID* 為 **int**。  
  
 *@cleartext*  
 為 **nvarchar**、**char**、**varchar** 或 **nchar** 類型的變數，其中包含將簽署的資料。  
  
 **'** *password* **'**  
 這是用來加密憑證私密金鑰的密碼。 *password* 為 **nvarchar(128)**。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary**，大小上限為 8,000 位元組。  
  
## <a name="remarks"></a>Remarks  
 需要憑證的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例使用憑證 `ABerglundCert07` 簽署 `@SensitiveData` 中的文字，且先使用密碼 "pGFD4bb925DGvbd2439587y" 將憑證解密。 然後將純文字和簽章插入資料表 `SignedData04`。  
  
```  
DECLARE @SensitiveData nvarchar(max);  
SET @SensitiveData = N'Saddle Price Points are   
    2, 3, 5, 7, 11, 13, 17, 19, 23, 29';  
INSERT INTO [SignedData04]  
    VALUES( N'data signed by certificate ''ABerglundCert07''',  
    @SensitiveData, SignByCert( Cert_Id( 'ABerglundCert07' ),   
    @SensitiveData, N'pGFD4bb925DGvbd2439587y' ));  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [VERIFYSIGNEDBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/verifysignedbycert-transact-sql.md)   
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
