---
title: "SIGNBYCERT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b753e29b576d70b8c77dc40b570ab10dc314f22e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="signbycert-transact-sql"></a>SIGNBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  以憑證簽署文字並傳回簽章。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SignByCert ( certificate_ID , @cleartext [ , 'password' ] )  
```  
  
## <a name="arguments"></a>引數  
 *certificate_ID*  
 為目前資料庫中憑證的識別碼。 *certificate_ID*是**int**。  
  
 *@cleartext*  
 這類型的變數**nvarchar**， **char**， **varchar**，或**nchar**其中包含要簽署的資料。  
  
 **'** *密碼* **'**  
 這是用來加密憑證私密金鑰的密碼。 *密碼*是**nvarchar （128)**。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary** 8,000 個位元組的大小上限。  
  
## <a name="remarks"></a>備註  
 需要憑證的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例將文字登入`@SensitiveData`憑證`ABerglundCert07`，需要先解密密碼"pGFD4bb925DGvbd2439587y"的憑證。 然後將純文字和簽章插入資料表 `SignedData04`。  
  
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
 [VERIFYSIGNEDBYCERT & #40;TRANSACT-SQL & #41;](../../t-sql/functions/verifysignedbycert-transact-sql.md)   
 [CERT_ID & #40;TRANSACT-SQL & #41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE & #40;TRANSACT-SQL & #41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [卸除憑證 & #40;TRANSACT-SQL & #41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
