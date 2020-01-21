---
title: ALTER CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e333a149ca50531be3eb89b8b9d249ea4d5996b9
ms.sourcegitcommit: cc20a148c785ac43832f47d096fe53508a4b1940
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2020
ms.locfileid: "75871118"
---
# <a name="alter-certificate-transact-sql"></a>ALTER CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  變更用來加密憑證私密金鑰的密碼、移除私密金鑰，或在沒有時匯入私密金鑰。 將憑證的可用性改為 [!INCLUDE[ssSB](../../includes/sssb-md.md)]。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER CERTIFICATE certificate_name   
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY ( <private_key_spec> )  
    | WITH ACTIVE FOR BEGIN_DIALOG = { ON | OFF }  
  
<private_key_spec> ::=   
      {   
        { FILE = 'path_to_private_key' | BINARY = private_key_bits }  
         [ , DECRYPTION BY PASSWORD = 'current_password' ]  
         [ , ENCRYPTION BY PASSWORD = 'new_password' ]  
      }  
    |  
      {  
         [ DECRYPTION BY PASSWORD = 'current_password' ]  
         [ [ , ] ENCRYPTION BY PASSWORD = 'new_password' ]  
      }  
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
 這是資料庫中憑證的唯一識別名稱。  
  
 REMOVE PRIVATE KEY  
 指定私密金鑰不應該在資料庫中繼續維護。  
  
 WITH PRIVATE KEY 指定憑證的私密金鑰會載入到 SQL Server。

 FILE ='*path_to_private_key*'  
 指定通往私密金鑰的完整路徑 (包括檔案名稱)。 這個參數可以是本機路徑或是通往網路位置的 UNC 路徑。 這個檔案會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶的安全性內容中被存取。 當您使用這個選項時，請確定服務帳戶有權存取指定的檔案。
 
 如果只指定檔案名稱，該檔案會儲存在執行個體的預設使用者資料夾中。 此資料夾不一定是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA 資料夾。 如果是 SQL Server Express LocalDB，執行個體的預設使用者資料夾是 `%USERPROFILE%` 環境變數為建立該執行個體的帳戶所指定的路徑。  
  
 BINARY ='*private_key_bits*'  
 **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。  
  
 指定為二進位常數的私密金鑰位元。 這些位元可以是加密形式。 如果加密的話，使用者必須提供解密密碼。 不會針對這個密碼執行密碼原則檢查。 私密金鑰位元應該採用 PVK 檔案格式。  
  
 DECRYPTION BY PASSWORD ='*current_password*'  
 指定私密金鑰解密所需的密碼。  
  
 ENCRYPTION BY PASSWORD ='*new_password*'  
 指定用來加密資料庫內憑證之私密金鑰的密碼。 *new_password* 必須符合執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之電腦的 Windows 密碼原則需求。 如需詳細資訊，請參閱＜ [Password Policy](../../relational-databases/security/password-policy.md)＞。  
  
 ACTIVE FOR BEGIN_DIALOG **=** { ON | OFF }  
 讓 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對話交談的起始端能夠使用該憑證。  
  
## <a name="remarks"></a>備註  
 私密金鑰必須對應至 *certificate_name* 所指定的公開金鑰。  
  
 如果您利用 Null 密碼來保護檔案中的密碼，就可以省略 DECRYPTION BY PASSWORD 子句。  
  
 匯入已存在於資料庫中的憑證私密金鑰時，私密金錀會自動受到資料庫主要金鑰的保護。 若要利用密碼來保護私密金鑰，請使用 ENCRYPTION BY PASSWORD 子句。  
  
 REMOVE PRIVATE KEY 選項會從資料庫刪除憑證的私密金鑰。 您可以在利用憑證來驗證簽章時，或在不需要私密金鑰的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 案例中，移除私密金鑰。 請勿移除保護對稱金鑰之憑證的私密金鑰。 必須還原私密金鑰，才能簽署應該使用憑證驗證的任何其他模組或字串，或解密已使用該憑證加密的值。   
  
 如果私密金鑰是利用資料庫主要金鑰加密時，就不必指定解密密碼。  
 
 若要變更用來加密私密金鑰的密碼，請勿指定 FILE 或 BINARY 子句。
  
> [!IMPORTANT]  
>  在從資料庫移除私密金鑰之前，請務必先製作一份保存副本。 如需詳細資訊，請參閱 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md) 及 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)。  
  
 自主資料庫無法使用 WITH PRIVATE KEY 選項。  
  
## <a name="permissions"></a>權限  
 需要憑證的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-removing-the-private-key-of-a-certificate"></a>A. 移除憑證的私密金鑰  
  
```  
ALTER CERTIFICATE Shipping04   
    REMOVE PRIVATE KEY;  
GO  
```  
  
### <a name="b-changing-the-password-that-is-used-to-encrypt-the-private-key"></a>B. 變更為私密金鑰加密所用的密碼  
  
```  
ALTER CERTIFICATE Shipping11   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hkjdskghFDGGG4%',  
    ENCRYPTION BY PASSWORD = '34958tosdgfkh##38');  
GO  
```  
  
### <a name="c-importing-a-private-key-for-a-certificate-that-is-already-present-in-the-database"></a>C. 匯入已在資料庫中之憑證的私密金鑰。  
  
```  
ALTER CERTIFICATE Shipping13   
    WITH PRIVATE KEY (FILE = 'c:\importedkeys\Shipping13',  
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
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)  
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
 [CERTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/certproperty-transact-sql.md)  
  
  

