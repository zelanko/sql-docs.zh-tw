---
description: CERTPROPERTY (Transact-SQL)
title: CERTPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: bbba412b97f88d52afa9a304c3cbbb101f74772b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88367274"
---
# <a name="certproperty-transact-sql"></a>CERTPROPERTY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回指定憑證屬性的值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```syntaxsql
CertProperty ( Cert_ID , '<PropertyName>' )  
  
<PropertyName> ::=  
   Expiry_Date | Start_Date | Issuer_Name   
   | Cert_Serial_Number | Subject | SID | String_SID   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
*Cert_ID*  
int 資料類型的憑證識別碼值。
  
*Expiry_Date*  
憑證到期日期。
  
*Start_Date*  
憑證生效的日期。
  
*Issuer_Name*  
憑證簽發者名稱。
  
*Cert_Serial_Number*  
憑證序號。
  
*主旨*  
憑證主體。
  
 *SID*  
憑證 SID。 這也是對應至這個憑證之任何登入或使用者的 SID。
  
*String_SID*  
字元字串格式的憑證 SID。 這也是對應至憑證之任何登入或使用者的 SID。
  
## <a name="return-types"></a>傳回類型
必須使用單引號括住屬性規格。
  
傳回類型取決於函式呼叫中所指定的屬性。 傳回類型 **sql_variant** 會包裝所有傳回值。
-   *Expiry_Date* 及 *Start_Date* 會傳回 **datetime**。  
-   *Cert_Serial_Number*、*Issuer_Name*、*String_SID* 和 *Subject* 全部會傳回 **nvarchar**。  
-   *SID* 會傳回 **varbinary**。  
  
## <a name="remarks"></a>備註  
請在 [sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 目錄檢視中查看憑證資訊。
  
## <a name="permissions"></a>權限  
需要憑證的適當權限，並且需要呼叫端尚未拒絕憑證的 VIEW 權限。 如需憑證權限的詳細資訊，請參閱 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md) 和 [GRANT CERTIFICATE PERMISSIONS &#40;Transact-SQL&#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)。
  
## <a name="examples"></a>範例  
下列範例會傳回憑證主旨。
  
```sql
-- First create a certificate.  
CREATE CERTIFICATE Marketing19 WITH   
    START_DATE = '04/04/2004' ,  
    EXPIRY_DATE = '07/07/2040' ,  
    SUBJECT = 'Marketing Print Division';  
GO  
  
-- Now use CertProperty to examine certificate  
-- Marketing19's properties.  
DECLARE @CertSubject sql_variant;  
set @CertSubject = CertProperty( Cert_ID('Marketing19'), 'Subject');  
PRINT CONVERT(nvarchar, @CertSubject);  
GO  
```  
  
## <a name="see-also"></a>請參閱
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)  
[CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)
[加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
[安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  
