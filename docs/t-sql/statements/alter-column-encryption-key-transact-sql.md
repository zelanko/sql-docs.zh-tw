---
title: "ALTER COLUMN ENCRYPTION KEY (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER COLUMN ENCRYPTION
- ALTER_COLUMN_ENCRYPTION_TSQL
- ALTER COLUMN ENCRYPTION KEY
- ALTER_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column encryption key, alter
- ALTER COLUMN ENCRYPTION KEY statement
ms.assetid: c79a220d-e178-4091-a330-c924cc0f0ae0
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6aaa1f85f860272cdb672d29bccdda39380f728a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-column-encryption-key-transact-sql"></a>ALTER COLUMN ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  改變資料行加密金鑰在資料庫中，加入或卸除加密的值。 CEK 可以有兩個值可以針對對應的資料行主要金鑰輪替。 當 CEK 加密使用的資料行時，會使用[永遠加密 &#40; Database engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)功能。 然後再加入 CEK 值，您必須定義用來加密所使用的值資料行主要金鑰[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或[CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)陳述式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ALTER COLUMN ENCRYPTION KEY key_name   
    [ ADD | DROP ] VALUE   
    (  
        COLUMN_MASTER_KEY = column_master_key_name   
        [, ALGORITHM = 'algorithm_name' , ENCRYPTED_VALUE =  varbinary_literal ]   
    ) [;]  
```  
  
## <a name="arguments"></a>引數  
 *key_name*  
 您要變更資料行加密金鑰。  
  
 *column_master_key_name*  
 指定用來加密資料行加密金鑰 (CEK) 的資料行主要金鑰 (CMK) 的名稱。  
  
 *algorithm_name*  
 用來加密值的加密演算法的名稱。 系統提供者的演算法必須是**RSA_OAEP**。 當卸除資料行加密金鑰值，這個引數無效。  
  
 *varbinary_literal*  
 與指定的主要加密金鑰加密 CEK BLOB。 執行個體時提供 SQL Server 登入。 當卸除資料行加密金鑰值，這個引數無效。  
  
> [!WARNING]  
>  絕對不要將傳遞純文字 CEK 值在這個陳述式。 這樣將會包含這項功能的好處。  
  
## <a name="remarks"></a>備註  
 一般來說，資料行加密金鑰會建立一個加密值。 當資料行主要金鑰必須要旋轉 （目前資料行主要金鑰必須換成新的資料行主要金鑰），您可以加入新的資料行加密金鑰值以新的資料行主要金鑰加密。 這可讓您確保用戶端應用程式可以存取新的資料行主要金鑰可使用用戶端應用程式時，資料行加密金鑰加密的資料。 啟用 永遠加密驅動程式沒有存取新的主要金鑰，將無法使用舊的資料行主要金鑰的加密資料行的加密金鑰值來存取敏感性資料的用戶端應用程式中。 加密演算法，永遠加密的支援，需要有 256 位元的純文字值。 應該使用金鑰存放區提供者所封裝的保存資料行主要金鑰的金鑰存放區產生的加密的值。  
  
 使用[sys.columns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)， [sys.column_encryption_keys &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)和[sys.column_encryption_key_values &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)來檢視資料行加密金鑰的相關資訊。  
  
## <a name="permissions"></a>Permissions  
 需要**ALTER ANY COLUMN ENCRYPTION KEY**資料庫的權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-adding-a-column-encryption-key-value"></a>A. 加入資料行加密金鑰值  
 下列範例會改變稱為資料行加密金鑰`MyCEK`。  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
ADD VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK2,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E00740075007300650072002F006D0079002F0064006500650063006200660034006100340031003000380034006200350033003200360066003200630062006200350030003600380065003900620061003000320030003600610037003800310066001DDA6134C3B73A90D349C8905782DD819B428162CF5B051639BA46EC69A7C8C8F81591A92C395711493B25DCBCCC57836E5B9F17A0713E840721D098F3F8E023ABCDFE2F6D8CC4339FC8F88630ED9EBADA5CA8EEAFA84164C1095B12AE161EABC1DF778C07F07D413AF1ED900F578FC00894BEE705EAC60F4A5090BBE09885D2EFE1C915F7B4C581D9CE3FDAB78ACF4829F85752E9FC985DEB8773889EE4A1945BD554724803A6F5DC0A2CD5EFE001ABED8D61E8449E4FAA9E4DD392DA8D292ECC6EB149E843E395CDE0F98D04940A28C4B05F747149B34A0BAEC04FFF3E304C84AF1FF81225E615B5F94E334378A0A888EF88F4E79F66CB377E3C21964AACB5049C08435FE84EEEF39D20A665C17E04898914A85B3DE23D56575EBC682D154F4F15C37723E04974DB370180A9A579BC84F6BC9B5E7C223E5CBEE721E57EE07EFDCC0A3257BBEBF9ADFFB00DBF7EF682EC1C4C47451438F90B4CF8DA709940F72CFDC91C6EB4E37B4ED7E2385B1FF71B28A1D2669FBEB18EA89F9D391D2FDDEA0ED362E6A591AC64EF4AE31CA8766C259ECB77D01A7F5C36B8418F91C1BEADDD4491C80F0016B66421B4B788C55127135DA2FA625FB7FD195FB40D90A6C67328602ECAF3EC4F5894BFD84A99EB4753BE0D22E0D4DE6A0ADFEDC80EB1B556749B4A8AD00E73B329C95827AB91C0256347E85E3C5FD6726D0E1FE82C925D3DF4A9  
);  
GO  
  
```  
  
### <a name="b-dropping-a-column-encryption-key-value"></a>B. 卸除資料行加密金鑰值  
 下列範例會改變稱為資料行加密金鑰`MyCEK`卸除的值。  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
DROP VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK  
);  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [卸除資料行加密金鑰 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  

