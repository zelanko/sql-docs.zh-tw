---
title: "建立憑證 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTIFICATE
- CREATE_CERTIFICATE_TSQL
- sql13.swb.createcertificate.f1
- CERTIFICATE_TSQL
- CREATE CERTIFICATE
- sql13.swb.certificateproperties.f1
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- certificates [SQL Server], adding
- certificates [SQL Server]
- adding certificates
- cryptography [SQL Server], certificates
- CREATE CERTIFICATE statement
ms.assetid: a4274b2b-4cb0-446a-a956-1c8e6587515d
caps.latest.revision: 74
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8753e820278eb04fff6f12e405d766fff5292e58
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-certificate-transact-sql"></a>CREATE CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  將憑證加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中。  
  
 此功能與使用資料層應用程式架構 (DACFx) 的資料庫匯出不相容。 您必須在匯出之前先卸除所有憑證。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE CERTIFICATE certificate_name [ AUTHORIZATION user_name ]   
    { FROM <existing_keys> | <generate_new_keys> }  
    [ ACTIVE FOR BEGIN_DIALOG =  { ON | OFF } ]  
  
<existing_keys> ::=   
    ASSEMBLY assembly_name  
    | {   
        [ EXECUTABLE ] FILE = 'path_to_file'  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]   
      }  
    | {   
        BINARY = asn_encoded_certificate  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]  
      }  
<generate_new_keys> ::=   
    [ ENCRYPTION BY PASSWORD = 'password' ]   
    WITH SUBJECT = 'certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<private_key_options> ::=  
      {   
        FILE = 'path_to_private_key'  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
    |  
      {   
        BINARY = private_key_bits  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
  
<date_options> ::=  
    START_DATE = 'datetime' | EXPIRY_DATE = 'datetime'  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CERTIFICATE certificate_name   
    { <generate_new_keys> | FROM <existing_keys> }  
    [ ; ]  
  
<generate_new_keys> ::=   
    WITH SUBJECT ='certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<existing_keys> ::=   
    {   
      FILE ='path_to_file'  
      WITH PRIVATE KEY   
         (   
           FILE ='path_to_private_key'  
           , DECRYPTION BY PASSWORD ='password'   
         )  
    }  
  
<date_options> ::=  
    START_DATE ='datetime' | EXPIRY_DATE ='datetime'  
```  
  
## <a name="arguments"></a>引數  
 *certificate_name*  
 是在資料庫中憑證的名稱。  
  
 授權*user_name*  
 是擁有此憑證名稱。  
  
 組件*assembly_name*  
 指定已載入資料庫中之簽署的組件。  
  
 [可執行檔]檔案 ='*path_to_file*'  
 指定包含憑證之 DER 編碼檔案的完整路徑，包括檔案名稱。 如有使用 EXECUTABLE 選項，該檔案即是已經過憑證簽署的 DLL。 *path_to_file*可以是本機路徑或通往網路位置的 UNC 路徑。 對檔案的安全性內容中存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶。 這個帳戶必須有所需的檔案系統權限。  
  
 WITH PRIVATE KEY  
 指定憑證的私密金鑰必須載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。 只有在從檔案建立憑證的情況下，這個子句才有效。 若要載入的組件的私密金鑰，使用[ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md)。  
  
 檔案 ='*path_to_private_key*'  
 指定通往私密金鑰的完整路徑 (包括檔案名稱)。 *path_to_private_key*可以是本機路徑或通往網路位置的 UNC 路徑。 對檔案的安全性內容中存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶。 這個帳戶必須有必要的檔案系統權限。  
  
> [!NOTE]  
>  自主資料庫無法使用這個選項。  
  
 asn_encoded_certificate  
 指定為二進位常數的 ASN 編碼憑證位元。  
  
 二進位 =*private_key_bits*  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定為二進位常數的私密金鑰位元。 這些位元可以是加密形式。 如果加密的話，使用者必須提供解密密碼。 不會針對這個密碼執行密碼原則檢查。 私密金鑰位元應該採用 PVK 檔案格式。  
  
 DECRYPTION BY PASSWORD ='*key_password*'  
 指定解密從檔案擷取的私密金鑰時所需的密碼。 如果私密金鑰由 Null 密碼保護，則這個子句是選擇性的。 建議您不要將私密金鑰儲存至一個沒有密碼保護的檔案。 如果密碼是必要的但沒有指定密碼，陳述式將會失敗。  
  
 ENCRYPTION BY PASSWORD ='*密碼*'  
 指定用來加密私密金鑰的密碼。 請只在您要利用密碼來加密憑證時才使用這個選項。 如果省略這個子句，則是使用資料庫主要金鑰來加密私用金鑰。 *密碼*必須符合正在執行的執行個體之電腦的 Windows 密碼原則需求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱＜ [Password Policy](../../relational-databases/security/password-policy.md)＞。  
  
 主體 ='*certificate_subject_name*'  
 詞彙*主旨*X.509 標準中所定義之憑證中繼資料中的欄位參考。 主體應該不能超過 64 個字元，以及對強制執行這項限制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]on Linux。 如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 Windows 中，主體可以是最多 128 個字元長度。 它們會儲存在目錄中，但是二進位大型物件 (BLOB) 包含憑證會保留完整的主旨名稱，會截斷超過 128 個字元的主旨。  
  
 START_DATE ='*datetime*'  
 這是憑證生效的日期。 如果未指定，START_DATE 設為等於目前的日期。 START_DATE 為 UTC 時間，可以用任何可轉換成日期和時間的格式指定。  
  
 EXPIRY_DATE ='*datetime*'  
 這是憑證到期的日期。 如果未指定，會將 EXPIRY_DATE 設 START_DATE 之後一年的日期。 EXPIRY_DATE 為 UTC 時間，可以用任何可轉換成日期和時間的格式指定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Service Broker 會檢查到期日。 不過，到期日不會強制執行憑證是用來進行加密。  
  
 ACTIVE FOR BEGIN_DIALOG = { **ON** |OFF}  
 讓 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對話交談的起始端能夠使用該憑證。 預設值是 ON。  
  
## <a name="remarks"></a>備註  
 憑證是遵照 X.509 標準及支援 X.509 V1 欄位的資料庫層級安全性實體。 CREATE CERTIFICATE 可以從檔案或組件載入憑證。 這個陳述式也可以產生金鑰組及建立自簽憑證。  
  
 必須是私用金鑰\<= 2500 個位元組，以加密格式。 產生的私密金鑰[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]為 1024 個位元長透過[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]且 2048 位元開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 從外部來源匯入的私密金鑰，其最小長度為 384 個位元，其最大長度為 4,096 個位元。 匯入的私密金鑰，其長度必須為 64 個位元的整數倍。 用於 TDE 的憑證限制在 3456 位元的私密金鑰大小。  
  
 整個序號的憑證會儲存，但是只有前 16 個位元組會出現在 sys.certificates 目錄檢視。  
  
 儲存憑證的整個簽發者欄位，但只有前 884 位元組 sys.certificates 目錄檢視。  
  
 私密金鑰必須對應到所指定的公開金鑰*certificate_name*。  
  
 當您從容器建立憑證時，載入私密金鑰是選擇性的。 但是當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生自簽憑證時，永遠會建立私密金鑰。 依預設，私密金鑰是利用資料庫主要金鑰來加密的。 如果資料庫主要金鑰不存在，而且沒有指定密碼，陳述式將會失敗。  
  
 利用資料庫主要金鑰加密的私密金鑰時，不需要 ENCRYPTION BY PASSWORD 選項。 私密金鑰利用密碼加密時，才使用此選項。 如果未指定密碼，則會利用資料庫主要金鑰加密憑證的私密金鑰。 如果無法開啟資料庫主要金鑰，請省略這個子句會造成錯誤。  
  
 如果是利用資料庫主要金鑰加密私密金鑰，就不必指定解密密碼。  
  
> [!NOTE]  
>  用於加密及簽署的內建函數不會檢查憑證的到期日期。 這些函數的使用者必須決定何時檢查憑證到期日期。  
  
 憑證的二進位描述可以建立使用[CERTENCODED &#40;TRANSACT-SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md)和[CERTPRIVATEKEY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/certprivatekey-transact-sql.md)函式。 如需範例，會使用**CERTPRIVATEKEY**和**CERTENCODED**將憑證複製到另一個資料庫，請參閱本主題中的範例 B [CERTENCODED &#40;TRANSACT-SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 CREATE CERTIFICATE 權限。 只有 Windows 登入、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入，以及應用程式角色可以擁有憑證。 群組和角色無法擁有憑證。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-self-signed-certificate"></a>A. 建立自我簽署憑證  
 下列範例會建立一個稱為 `Shipping04` 的憑證。 這個憑證的私密金鑰是利用密碼來保護的。  
  
```  
CREATE CERTIFICATE Shipping04   
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
   WITH SUBJECT = 'Sammamish Shipping Records',   
   EXPIRY_DATE = '20201031';  
GO  
```  
  
### <a name="b-creating-a-certificate-from-a-file"></a>B. 從檔案建立憑證  
 下列範例在資料庫中建立憑證，並從檔案載入金鑰組。  
  
```  
CREATE CERTIFICATE Shipping11   
    FROM FILE = 'c:\Shipping\Certs\Shipping11.cer'   
    WITH PRIVATE KEY (FILE = 'c:\Shipping\Certs\Shipping11.pvk',   
    DECRYPTION BY PASSWORD = 'sldkflk34et6gs%53#v00');  
GO   
```  
  
### <a name="c-creating-a-certificate-from-a-signed-executable-file"></a>C. 從簽署的可執行檔建立憑證  
  
```  
CREATE CERTIFICATE Shipping19   
    FROM EXECUTABLE FILE = 'c:\Shipping\Certs\Shipping19.dll';  
GO  
```  
  
 另外，您也可以從 `dll` 檔建立組件，然後從該組件建立憑證。  
  
```  
CREATE ASSEMBLY Shipping19   
    FROM ' c:\Shipping\Certs\Shipping19.dll'   
    WITH PERMISSION_SET = SAFE;  
GO  
CREATE CERTIFICATE Shipping19 FROM ASSEMBLY Shipping19;  
GO  
```  
  
### <a name="d-creating-a-self-signed-certificate"></a>D. 建立自我簽署憑證  
 下列範例會建立稱為憑證`Shipping04`但未指定加密密碼。 這個範例可以搭配[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。
  
```  
CREATE CERTIFICATE Shipping04   
   WITH SUBJECT = 'Sammamish Shipping Records';  
GO  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [ALTER CERTIFICATE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [卸除憑證 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [CERTENCODED &#40;TRANSACT-SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md)   
 [CERTPRIVATEKEY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
  
  



