---
title: Always Encrypted 密碼編譯 | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, cryptography system
ms.assetid: ae8226ff-0853-4716-be7b-673ce77dd370
author: aliceku
ms.author: aliceku
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 70a18e569b43066bd64fe56593c47980a6894b09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043294"
---
# <a name="always-encrypted-cryptography"></a>永遠加密的密碼編譯
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  本文件描述加密演算法和機制，以衍生在 [和](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) 上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 永遠加密 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)]功能中使用的密碼編譯內容。  
  
## <a name="keys-key-stores-and-key-encryption-algorithms"></a>金鑰、金鑰存放區及金鑰加密演算法
 Always Encrypted 使用兩種金鑰類型：資料行主要金鑰和資料行加密金鑰。  
  
 資料行主要金鑰 (CMK) 是加密金鑰的金鑰 (也就是用來加密其它金鑰的金鑰)，其一律會由用戶端控制，並儲存於外部金鑰存放區中。 已啟用「永遠加密」的用戶端驅動程式會透過 CMK 存放區提供者來與金鑰存放區互動，其可以是驅動程式庫 ( [!INCLUDE[msCoName](../../../includes/msconame-md.md)]/系統提供者) 的一部分或用戶端應用程式 (自訂提供者) 的一部分。 用戶端驅動程式庫目前包括適用於 [Windows 憑證存放區](/windows/desktop/SecCrypto/using-certificate-stores) 的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 金鑰存放區提供者和硬體安全性模組 (HSM)  (如需目前的提供者清單，請參閱 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md))。應用程式開發人員可以針對任意存放區提供自訂提供者。  
  
 資料行加密金鑰 (CEK) 是受到 CMK 保護的內容加密金鑰 (例如：用來保護資料的金鑰)。  
  
 所有 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] CMK 存放區提供者都會使用具備最佳非對稱加密填補的 RSA (RSA-OAEP) 來加密 CEK。 支援 Microsoft Cryptography API 的金鑰存放區提供者包括：.NET Framework 中的新一代 (CNG) ([SqlColumnEncryptionCngProvider 類別](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncngprovider.aspx)) 使用 RFC 8017 在第 A.2.1 節指定的預設參數。 這些預設參數會使用 SHA-1 的雜湊函數，以及搭配 SHA-1 的 MGF1 遮罩產生函數。 所有其它的金鑰存放區提供者都使用 SHA-256。 
  
## <a name="data-encryption-algorithm"></a>資料加密演算法  
 「永遠加密」會使用 **AEAD_AES_256_CBC_HMAC_SHA_256** 演算法來加密資料庫中的資料。  
  
 **AEAD_AES_256_CBC_HMAC_SHA_256** 衍生自 [https://tools.ietf.org/html/draft-mcgrew-aead-aes-cbc-hmac-sha2-05](https://tools.ietf.org/html/draft-mcgrew-aead-aes-cbc-hmac-sha2-05) 的規格草稿。 它會使用「驗證的加密」配置搭配相關聯的資料，遵循「加密然後 MAC」方法。 那就是，第一次加密純文字，並根據產生的加密文字產生 MAC。  
  
 為了隱藏模式， **AEAD_AES_256_CBC_HMAC_SHA_256** 會使用作業的加密區塊鏈結 (CBC) 模式，其中會將初始值送入名為初始化向量 (IV) 的系統中。 CBC 模式的完整描述請參閱 [https://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf](https://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf)。  
  
 **AEAD_AES_256_CBC_HMAC_SHA_256** 會使用下列步驟，來計算指定純文字值的加密文字值。  
  
### <a name="step-1-generating-the-initialization-vector-iv"></a>步驟 1:產生初始化向量 (IV)  
 「永遠加密」支援 **AEAD_AES_256_CBC_HMAC_SHA_256**的兩種變化：  
  
-   隨機化  
  
-   具決定性  
  
 如果是隨機化加密，就會隨機產生 IV。 因此，每次加密相同的純文字時，都會產生不同的加密文字，這樣可防止任何資訊外洩。  
  
```  
When using randomized encryption: IV = Generate cryptographicaly random 128bits  
```  
  
 若有具確定性的加密，便不會隨機產生 IV，而是會使用以下演算法從純文字的值衍生：  
  
```  
When using deterministic encryption: IV = HMAC-SHA-256( iv_key, cell_data ) truncated to 128 bits.  
```  
  
 其中 iv_key 會以下列方式衍生自 CEK︰  
  
```  
iv_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell IV key" + algorithm + CEK_length)  
```  
  
 執行 HMAC 值截斷以使其可以容納在 IV 所需要的 1 個資料區塊中。
因此，具決定性加密一律會針對指定的純文字值產生相同加密文字，這樣就能藉由比較兩個純文字值的對應加密文字值，來推斷其是否相等。 這個有限度的資料洩漏，讓資料庫系統能夠支援已加密資料行值上的相等比較。  
  
 相較於替代項目，具決定性加密在隱藏模式中更具效率，例如使用預先定義的 IV 值。  
  
### <a name="step-2-computing-aes256cbc-ciphertext"></a>步驟 2:計算 AES_256_CBC 加密文字  
 計算 IV 之後，即會產生 **AES_256_CBC** 加密文字︰  
  
```  
aes_256_cbc_ciphertext = AES-CBC-256(enc_key, IV, cell_data) with PKCS7 padding.  
```  
  
 其中的加密金鑰 (enc_key) 是衍生自 CEK，如下所示。  
  
```  
enc_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell encryption key" + algorithm + CEK_length )  
```  
  
### <a name="step-3-computing-mac"></a>步驟 3：計算 MAC  
 接著，使用下列演算法來計算 MAC︰  
  
```  
MAC = HMAC-SHA-256(mac_key, versionbyte + IV + Ciphertext + versionbyte_length)  
```  
  
 其中：  
  
```  
versionbyte = 0x01 and versionbyte_length = 1
mac_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell MAC key" + algorithm + CEK_length)  
```  
  
### <a name="step-4-concatenation"></a>步驟 4：串連  
 最後，會透過將演算法版本位元組、MAC、IV 和 AES_256_CBC 加密文字串連，來產生加密值：  
  
```  
aead_aes_256_cbc_hmac_sha_256 = versionbyte + MAC + IV + aes_256_cbc_ciphertext  
```  
  
## <a name="ciphertext-length"></a>加密文字長度  
 **AEAD_AES_256_CBC_HMAC_SHA_256** 加密文字的特定元件長度 (以位元組為單位) 如下︰  
  
-   versionbyte：1  
  
-   MAC: 32  
  
-   IV: 16  
  
-   aes_256_cbc_ciphertext︰ `(FLOOR (DATALENGTH(cell_data)/ block_size) + 1)* block_size`，其中︰  
  
    -   block_size 是 16 位元組  
  
    -   cell_data 是純文字值  
  
     因此，aes_256_cbc_ciphertext 的最小大小為 1 個區塊，也就是 16 個位元組。  
  
 您因而可使用以下公式來計算加密文字 (因為加密指定的純文字值 (cell_data) 而產生) 的長度︰  
  
```  
1 + 32 + 16 + (FLOOR(DATALENGTH(cell_data)/16) + 1) * 16  
```  
  
 例如：  
  
-   加密之後，4 個位元組長的 **int** 純文字值會變成 65 個位元組長的二進位值。  
  
-   加密之後，2,000 個位元組長的 **nchar(1000)** 純文字值會變成 2,065 個位元組長的二進位值。  
  
 下表包含資料類型的完整清單以及每個類型的加密文字長度。  
  
|資料類型|加密文字長度 [位元組]|  
|---------------|---------------------------------|  
|**bigint**|65|  
|**binary**|變動。 使用上述公式。|  
|**bit**|65|  
|**char**|變動。 使用上述公式。|  
|**date**|65|  
|**datetime**|65|  
|**datetime2**|65|  
|**datetimeoffset**|65|  
|**decimal**|81|  
|**float**|65|  
|**地理位置**|N/A (不支援)|  
|**幾何**|N/A (不支援)|  
|**hierarchyid**|N/A (不支援)|  
|**image**|N/A (不支援)|  
|**int**|65|  
|**money**|65|  
|**nchar**|變動。 使用上述公式。|  
|**ntext**|N/A (不支援)|  
|**numeric**|81|  
|**nvarchar**|變動。 使用上述公式。|  
|**real**|65|  
|**smalldatetime**|65|  
|**smallint**|65|  
|**smallmoney**|65|  
|**sql_variant**|N/A (不支援)|  
|**sysname**|N/A (不支援)|  
|**text**|N/A (不支援)|  
|**time**|65|  
|**timestamp**<br /><br /> (**rowversion**)|N/A (不支援)|  
|**tinyint**|65|  
|**uniqueidentifier**|81|  
|**varbinary**|變動。 使用上述公式。|  
|**varchar**|變動。 使用上述公式。|  
|**xml**|N/A (不支援)|  
  
## <a name="net-reference"></a>.NET 參考  
 如需本文件所討論的演算法詳細資訊，請參閱 **.NET 參考** 中的 **SqlAeadAes256CbcHmac256Algorithm.cs** 和 [SqlColumnEncryptionCertificateStoreProvider.cs](https://referencesource.microsoft.com/)檔案。  
  
## <a name="see-also"></a>另請參閱  
 [永遠加密 &#40;Database Engine&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [永遠加密 &#40;用戶端開發&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
