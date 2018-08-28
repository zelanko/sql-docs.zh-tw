---
title: ALTER CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/18/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_CERTIFICATE_TSQL
- ALTER CERTIFICATE
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- encryption [SQL Server], certificates
- modifying certificates
- private keys [SQL Server]
- ALTER CERTIFICATE statement
- certificates [SQL Server], modifying
ms.assetid: da4dc25e-72e0-4036-87ce-22de83160836
caps.latest.revision: 46
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d73be79f224a4d95e7c397b55ee1441d5d0cdd9
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43071363"
---
# <a name="alter-certificate-transact-sql"></a>ALTER CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  變更為憑證加密所用的私密金鑰，如果沒有，則加入一個。 將憑證的可用性改為 [!INCLUDE[ssSB](../../includes/sssb-md.md)]。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER CERTIFICATE certificate_name   
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY ( <private_key_spec> [ ,... ] )  
    | WITH ACTIVE FOR BEGIN_DIALOG = [ ON | OFF ]  
  
<private_key_spec> ::=   
      FILE = 'path_to_private_key'   
    | DECRYPTION BY PASSWORD = 'key_password'   
    | ENCRYPTION BY PASSWORD = 'password'   
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER CERTIFICATE certificate_name   
{  
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY (   
        FILE = '<path_to_private_key>',  
        DECRYPTION BY PASSWORD = '<key password>' )
}  
```  
  
## <a name="arguments"></a>引數  
 *certificate_name*  
 這是在資料庫中辨識憑證的唯一名稱。  
  
 FILE **='***path_to_private_key***'**  
 指定通往私密金鑰的完整路徑 (包括檔案名稱)。 這個參數可以是本機路徑或是通往網路位置的 UNC 路徑。 這個檔案會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶的安全性內容中被存取。 當您使用這個選項時，必須確定服務帳戶有權存取指定的檔案。  
  
 DECRYPTION BY PASSWORD **='***key_password***'**  
 指定私密金鑰解密所需的密碼。  
  
 ENCRYPTION BY PASSWORD **='***password***'**  
 指定用來加密資料庫內憑證之私密金鑰的密碼。 *password* 必須符合執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之電腦的 Windows 密碼原則需求。 如需詳細資訊，請參閱＜ [Password Policy](../../relational-databases/security/password-policy.md)＞。  
  
 REMOVE PRIVATE KEY  
 指定私密金鑰不應該在資料庫中繼續維護。  
  
 ACTIVE FOR BEGIN_DIALOG **=** { ON | OFF }  
 讓 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對話交談的起始端能夠使用該憑證。  
  
## <a name="remarks"></a>Remarks  
 私密金鑰必須對應至 *certificate_name* 所指定的公開金鑰。  
  
 如果您利用 Null 密碼來保護檔案中的密碼，就可以省略 DECRYPTION BY PASSWORD 子句。  
  
 從檔案匯入已存在於資料庫中之憑證的私密金鑰時，私密金錀會自動受到資料庫主要金鑰的保護。 若要利用密碼來保護私密金鑰，請使用 ENCRYPTION BY PASSWORD 片語。  
  
 REMOVE PRIVATE KEY 選項會從資料庫刪除憑證的私密金鑰。 您可以在利用憑證來驗證簽章時，或在不需要私密金鑰的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 案例中，移除私密金鑰。 請勿移除保護對稱金鑰之憑證的私密金鑰。  
  
 如果私密金鑰是利用資料庫主要金鑰加密時，就不必指定解密密碼。  
  
> [!IMPORTANT]  
>  在從資料庫移除私密金鑰之前，請務必先製作一份保存副本。 如需詳細資訊，請參閱 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)。  
  
 自主資料庫無法使用 WITH PRIVATE KEY 選項。  
  
## <a name="permissions"></a>[權限]  
 需要憑證的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-password-of-a-certificate"></a>A. 變更憑證的密碼  
  
```  
ALTER CERTIFICATE Shipping04   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = 'pGF$5DGvbd2439587y',  
    ENCRYPTION BY PASSWORD = '4-329578thlkajdshglXCSgf');  
GO  
```  
  
### <a name="b-changing-the-password-that-is-used-to-encrypt-the-private-key"></a>B. 變更為私密金鑰加密所用的密碼  
  
```  
ALTER CERTIFICATE Shipping11   
    WITH PRIVATE KEY (ENCRYPTION BY PASSWORD = '34958tosdgfkh##38',  
    DECRYPTION BY PASSWORD = '95hkjdskghFDGGG4%');  
GO  
```  
  
### <a name="c-importing-a-private-key-for-a-certificate-that-is-already-present-in-the-database"></a>C. 匯入已在資料庫中之憑證的私密金鑰。  
  
```  
ALTER CERTIFICATE Shipping13   
    WITH PRIVATE KEY (FILE = 'c:\\importedkeys\Shipping13',  
    DECRYPTION BY PASSWORD = 'GDFLKl8^^GGG4000%');  
GO  
```  
  
### <a name="d-changing-the-protection-of-the-private-key-from-a-password-to-the-database-master-key"></a>D. 將私密金鑰的保護，從密碼改為資料庫主要金鑰  
  
```  
ALTER CERTIFICATE Shipping15   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hk000eEnvjkjy#F%');  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

