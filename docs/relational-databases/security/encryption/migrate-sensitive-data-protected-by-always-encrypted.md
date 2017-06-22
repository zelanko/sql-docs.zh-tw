---
title: "移轉透過 Always Encrypted 保護的機密資料 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/04/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: da73d0d20404f513e22dcdf0340e24fe85dc3184
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="migrate-sensitive-data-protected-by-always-encrypted"></a>移轉透過永遠加密保護的機密資料
  若要在大量複製作業期間載入加密的資料而不需在伺服器上執行中繼資料檢查，請使用 **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** 選項來建立使用者。 此選項適用於比 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 還舊之 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 版本的舊版工具 (例如 bcp.exe)，或者利用無法使用「永遠加密」的協力廠商擷取-轉換-載入 (ETL) 工作流程來使用。 這可讓使用者將加密的資料從某一組資料表 (包含加密的資料行) 安全地移至另一組具有加密資料行 (位於相同或不同的資料庫) 的資料表。  
  
## <a name="the-allowencryptedvaluemodifications-option"></a>ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 選項  
 [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) 和 [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) 都具有 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 選項。 設為 ON (預設值為 OFF) 時，此選項會在大量複製作業中抑制伺服器上的密碼編譯中繼資料檢查，讓使用者不需解密資料，就能在資料表或資料庫之間大量複製加密的資料。  
  
## <a name="data-migration-scenarios"></a>資料移轉案例  
 下表顯示適用於數種移轉案例的建議設定。  
  
 ![always-encrypted-migration](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "always-encrypted-migration")  
  
## <a name="bulk-loading-of-encrypted-data"></a>大量載入加密資料  
 請使用下列程序來載入加密的資料。  
  
1.  針對資料庫中做為大量複製作業目標的使用者，將選項設為 ON。 例如：  
  
    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
    ```  
  
2.  執行以該使用者身分連接的大量複製應用程式或工具 (如果您的應用程式使用已啟用「永遠加密」的用戶端驅動程式，請確定資料來源的連接字串未包含 **column encryption setting=enabled** ，以確保從加密資料行擷取的資料仍會維持加密。 如需詳細資訊，請參閱 [永遠加密 &#40;用戶端開發&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md))。  
  
3.  將 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 選項設回 OFF。 例如：  
  
    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
    ```  
  
## <a name="potential-for-data-corruption"></a>資料損毀的可能性  
 不當使用這個選項會導致資料損毀。 **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** 選項可讓使用者在資料庫中將任何資料插入加密的資料行，包括使用不同金鑰加密、未正確加密，或完全不加密的資料。 如果使用者不小心使用了針對目標資料行設定的加密配置 (資料行加密金鑰、演算法、加密類型) 來複製未正確加密的資料，您將無法解密資料 (資料將會損毀)。 您必須謹慎使用這個選項，因為它會導致資料庫中的資料損毀。  
  
 下列案例示範未正確匯入資料如何導致資料損毀︰  
  
1.  針對使用者將選項設為 ON。  
  
2.  使用者執行連接至資料庫的應用程式。 應用程式使用大量 API，將純文字值插入加密的資料行。 應用程式預期已啟用「永遠加密」的用戶端驅動程式會在插入時加密資料。 不過，由於應用程式設定錯誤，因此，它最終會使用不支援「永遠加密」的驅動程式，或者連接字串未包含 **column encryption setting=enabled**。  
  
3.  應用程式會將純文字值傳送到伺服器。 針對使用者在伺服器中停用密碼編譯中繼資料檢查時，伺服器會將不正確的資料 (純文字，而不是正確加密的加密文字) 插入加密的資料行。  
  
4.  相同或其他的應用程式會使用已啟用「永遠加密」的驅動程式，且連接字串中含有 **column encryption setting=enabled** ，來連接資料庫並擷取資料。 應用程式預期資料會明確地進行解密。 不過，驅動程式無法解密資料，因為資料不是正確的加密文字。  
  
## <a name="best-practice"></a>最佳做法  
  
-   使用指定的使用者帳戶，利用此選項長時間執行工作負載。  
  
-   針對短時間執行且需要移動加密資料 (而不將其解密) 的大量複製應用程式或工具，在執行應用程式之前，即時將選項設為 ON，並在執行作業之後立即將它設回 OFF。  
  
-   不要使用此選項來開發新的應用程式。 請改用用戶端驅動程式 (例如 ADO 4.6.1)，提供 API 來抑制單一工作階段的密碼編譯中繼資料檢查。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
 [ALTER USER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   
 [永遠加密 &#40;Database Engine&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [永遠加密精靈](../../../relational-databases/security/encryption/always-encrypted-wizard.md)   
 [永遠加密 &#40;用戶端開發&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  

