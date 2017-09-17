---
title: "CERTPROPERTY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTPROPERTY
- CERTPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], schema names
- schemas [SQL Server], names
- CERTPROPERTY function
ms.assetid: 966c09aa-bc4e-45b0-ba53-c8381871f638
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b43b587688b574c6d6395b72c5b368b82e617fd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="certproperty-transact-sql"></a>CERTPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回指定憑證屬性的值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CertProperty ( Cert_ID , '<PropertyName>' )  
  
<PropertyName> ::=  
   Expiry_Date | Start_Date | Issuer_Name   
   | Cert_Serial_Number | Subject | SID | String_SID   
```  
  
## <a name="arguments"></a>引數  
*Cert_ID*  
這是憑證的識別碼。 *Cert_ID*為 int。
  
*Expiry_Date*  
這是憑證的到期日。
  
*Start_Date*  
這是憑證生效的日期。
  
*Issuer_Name*  
這是憑證的簽發者名稱。
  
*Cert_Serial_Number*  
這是憑證序號。
  
*主旨*  
這是憑證的主旨。
  
 *SID*  
這是憑證的 SID。 這也是對應至這個憑證之任何登入或使用者的 SID。
  
*String_SID*  
這是字元字串格式的憑證 SID。 這也是對應至憑證之任何登入或使用者的 SID。
  
## <a name="return-types"></a>傳回型別
屬性規格必須括在單引號中。
  
傳回類型會隨著函數呼叫中指定的屬性而不同。 所有傳回值會包裝在的傳回型別**sql_variant**。
-   *Expiry_Date*和*Start_Date*傳回**datetime**。  
-   *Cert_Serial_Number*， *Issuer_Name*，*主旨*，和*String_SID*傳回**nvarchar**。  
-   *SID*傳回**varbinary**。  
  
## <a name="remarks"></a>備註  
憑證的相關資訊會顯示在[sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)目錄檢視。
  
## <a name="permissions"></a>Permissions  
需要憑證的部份權限，且呼叫端尚未拒絕憑證的 VIEW DEFINITION 權限。
  
## <a name="examples"></a>範例  
下列範例會傳回憑證主旨。
  
```sql
-- First create a certificate.  
CREATE CERTIFICATE Marketing19 WITH   
    START_DATE = '04/04/2004' ,  
    EXPIRY_DATE = '07/07/2007' ,  
    SUBJECT = 'Marketing Print Division';  
GO  
  
-- Now use CertProperty to examine certificate  
-- Marketing19's properties.  
DECLARE @CertSubject sql_variant;  
set @CertSubject = CertProperty( Cert_ID('Marketing19'), 'Subject');  
PRINT CONVERT(nvarchar, @CertSubject);  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[ALTER CERTIFICATE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)  
[CERT_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cert-id-transact-sql.md) 
[加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)
[sys.certificates &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 
[安全性目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  

