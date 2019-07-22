---
title: 在兩部伺服器上建立相同的對稱金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- symmetric keys [SQL Server], creating
ms.assetid: a13d0b21-a43b-43c0-9c22-7ba8f3d15e80
author: aliceku
ms.author: aliceku
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9bcb4748aebe7b4e24ebfe8f857f422ac8a41f47
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049966"
---
# <a name="create-identical-symmetric-keys-on-two-servers"></a>在兩部伺服器上建立相同的對稱金鑰
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中於兩部不同的伺服器上建立相同的對稱金鑰 若要解密加密文字，您就需要用來加密的金鑰。 在單一資料庫中同時進行加密和解密時，此金鑰會儲存在資料庫中，然後根據權限提供金鑰，以便進行加密和解密。 但是，在不同的資料庫或不同的伺服器上進行加密和解密時，儲存在某個資料庫中的金鑰將無法在第二個資料庫上使用。
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="limitations-and-restrictions"></a>限制事項  
  
- 當建立對稱金鑰時，至少必須利用下列一項來加密對稱金鑰：憑證、密碼、對稱金鑰、非對稱金鑰或 PROVIDER。 針對每一種類型，金鑰都可以有多個加密。 換句話說，可以同時利用多個憑證、密碼、對稱金鑰及非對稱金鑰來加密單一對稱金鑰。  
  
- 如果是利用密碼 (而不是利用資料庫主要金鑰的公開金鑰) 來加密對稱金鑰，則會使用 TRIPLE DES 加密演算法。 因此，利用強式加密演算法 (如 AES) 建立的金鑰，其本身的安全是由較弱的演算法來維護的。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>權限  
 需要資料庫的 ALTER ANY SYMMETRIC KEY 權限。 如果指定了 AUTHORIZATION，則需要資料庫使用者的 IMPERSONATE 權限或應用程式角色的 ALTER 權限。 如果是利用憑證或非對稱金鑰來加密，則需要憑證或非對稱金鑰的 VIEW DEFINITION 權限。 只有 Windows 登入、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入，以及應用程式角色可以擁有對稱金鑰。 群組和角色無法擁有對稱金鑰。  
  
## <a name="using-transact-sql"></a>使用 Transact-SQL  
  
### <a name="to-create-identical-symmetric-keys-on-two-different-servers"></a>若要在兩部不同的伺服器上建立相同的對稱金鑰  
  
1. 在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2. 在標準列上，按一下 **[新增查詢]** 。  
  
3. 執行下列 CREATE MASTER KEY、CREATE CERTIFICATE 和 CREATE SYMMETRIC KEY 陳述式，建立金鑰。  
  
    ```sql
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'My p@55w0Rd';  
    GO  
    CREATE CERTIFICATE [cert_keyProtection] WITH SUBJECT = 'Key Protection';  
    GO  
    CREATE SYMMETRIC KEY [key_DataShare] WITH  
        KEY_SOURCE = 'My key generation bits. This is a shared secret!',  
        ALGORITHM = AES_256,   
        IDENTITY_VALUE = 'Key Identity generation bits. Also a shared secret'  
        ENCRYPTION BY CERTIFICATE [cert_keyProtection];  
    GO  
    ```  
  
4. 連接到另一個伺服器執行個體，開啟不同的查詢視窗，然後執行以上 SQL 陳述式，在第二部伺服器上建立相同的金鑰。  
  
5. 先在第一部伺服器上執行以下 OPEN SYMMETRIC KEY 陳述式和 SELECT 陳述式，藉以測試金鑰。  
  
    ```sql
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    SELECT encryptbykey(key_guid('key_DataShare'), 'MyData' )  
    GO  
    -- For example, the output might look like this: 0x2152F8DA8A500A9EDC2FAE26D15C302DA70D25563DAE7D5D1102E3056CE9EF95CA3E7289F7F4D0523ED0376B155FE9C3  
    ```  
  
6. 在第二部伺服器上，將之前 SELECT 陳述式的結果貼入下列程式碼，做為 `@blob` 的值，然後執行下列程式碼來確認重複金鑰可以解密加密文字。  
  
    ```sql
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    DECLARE @blob varbinary(8000);  
    SET @blob = SELECT CONVERT(varchar(8000), decryptbykey(@blob));  
    GO  
    ```  
  
7. 關閉兩部伺服器上的對稱金鑰。  
  
    ```sql
    CLOSE SYMMETRIC KEY [key_DataShare];  
    GO  
    ```  

### <a name="encryption-changes-in-sql-server-2017-cu2"></a>SQL Server 2017 CU2 中的加密變更

SQL Server 2016 使用 SHA1 雜湊演算法進行加密工作。 從 SQL Server 2017 開始，已改為使用 SHA2。 這表示可能需要額外的步驟，才能使您的 SQL Server 2017 安裝將 SQL Server 2016 所加密的項目解密。 額外的步驟如下：

- 確定您的 SQL Server 2017 至少已更新為累積更新 2 (CU2)。
  - 如需重要的詳細資料，請參閱 [SQL Server 2017 的累積更新 2 (CU2)](https://support.microsoft.com/help/4052574) \(機器翻譯\)。
- 安裝 CU2 之後，在 SQL Server 2017 中開啟追蹤旗標 4631：`DBCC TRACEON(4631, -1);`
  - 追蹤旗標 4631 是 SQL Sewrver 2017 的新功能。 您必須在全域中將追蹤旗標 4631 設定為 `ON`，然後才能在 SQL Server 2017 中建立主要金鑰、憑證或對稱金鑰。 這樣即可讓這些建立的項目能夠與 SQL Server 2016 及舊版進行相互操作。

如需詳細指引，請參閱：

- [修正：SQL Server 2017 無法使用相同的對稱金鑰來將舊版 SQL Server 所加密的資料解密](https://support.microsoft.com/help/4053407/sql-server-2017-cannot-decrypt-data-encrypted-by-earlier-versions) \(機器翻譯\)
- [相同的對稱金鑰無法在 SQL Server 2017 和其他 SQL Server 版本之間運作](https://feedback.azure.com/forums/908035-sql-server/suggestions/33116269-identical-symmetric-keys-do-not-work-between-sql-s) \(英文\) <!-- Issue 2225. Thank you Stephen W and Sam Rueby. -->

## <a name="for-more-information"></a>如需詳細資訊

-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)  
  
-   [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)  
  
-   [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)  
