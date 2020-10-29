---
title: 使用 Always Encrypted 將大量的加密資料載入資料行
description: 了解如何使用 Always Encrypted 與 SQL Server 將大量資料載入資料行。
ms.custom: seo-lt-2019
ms.date: 11/04/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 435c9e512278d3954c46e543ab6d68610f1cbdfc
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92679266"
---
# <a name="bulk-load-encrypted-data-to-columns-using-always-encrypted"></a>使用 Always Encrypted 將大量的加密資料載入資料行
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

若要在大量複製作業期間載入加密的資料而不需在伺服器上執行中繼資料檢查，請使用 **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** 選項來建立使用者。 此選項適用於無法使用 Always Encrypted 的舊版工具或第三方的擷取 - 轉換 - 載入 (ETL) 工作流程。 這可讓使用者將加密的資料從某一組資料表 (包含加密的資料行) 安全地移至另一組具有加密資料行 (位於相同或不同的資料庫) 的資料表。  

 ## <a name="the-allow_encrypted_value_modifications-option"></a>ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 選項  
 [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md) 和 [ALTER USER](../../../t-sql/statements/alter-user-transact-sql.md) 都具有 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 選項。 設為 ON (預設值為 OFF) 時，此選項會在大量複製作業中抑制伺服器上的密碼編譯中繼資料檢查，讓使用者不需解密資料，就能在資料表或資料庫之間大量複製加密的資料。  
  
## <a name="data-migration-scenarios"></a>資料移轉案例  
下表顯示適用於數種移轉案例的建議設定。  
 
![資料表的螢幕擷取畫面，其中顯示適用於數種移轉案例的建議設定。](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "永遠加密 - 移轉")  

## <a name="bulk-loading-of-encrypted-data"></a>大量載入加密資料  
請使用下列程序來載入加密的資料。  

1.  針對資料庫中做為大量複製作業目標的使用者，將選項設為 ON。 例如：  
 
   ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
   ```  

2.  執行以該使用者身分連接的大量複製應用程式或工具 (如果您的應用程式使用已啟用「永遠加密」的用戶端驅動程式，請確定資料來源的連接字串未包含 **column encryption setting=enabled** ，以確保從加密資料行擷取的資料仍會維持加密。 如需詳細資訊，請參閱[使用 Always Encrypted 開發應用程式](always-encrypted-client-development.md))。  
  
3.  將 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 選項設回 OFF。 例如：  

    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
    ```  

## <a name="potential-for-data-corruption"></a>資料損毀的可能性  
不當使用這個選項會導致資料損毀。 **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** 選項可讓使用者在資料庫中將任何資料插入加密的資料行，包括使用不同金鑰加密、未正確加密，或完全不加密的資料。 如果使用者不小心使用針對目標資料行所設定加密配置 (資料行加密金鑰、演算法、加密類型) 來複製未正確加密的資料，則您將無法解密資料 (資料將會損毀)。 您必須謹慎使用這個選項，因為它會導致資料庫中的資料損毀。  

下列案例示範未正確匯入資料如何導致資料損毀︰  

1.  針對使用者將選項設為 ON。  
 
2.  使用者執行連接至資料庫的應用程式。 應用程式使用大量 API，將純文字值插入加密的資料行。 應用程式預期已啟用「永遠加密」的用戶端驅動程式會在插入時加密資料。 不過，由於應用程式設定錯誤，因此，它最終會使用不支援「永遠加密」的驅動程式，或者連接字串未包含 **column encryption setting=enabled** 。  

3.  應用程式會將純文字值傳送到伺服器。 針對使用者在伺服器中停用密碼編譯中繼資料檢查時，伺服器會將不正確的資料 (純文字，而不是正確加密的加密文字) 插入加密的資料行。  
 
4.  相同或其他的應用程式會使用已啟用「永遠加密」的驅動程式，且連接字串中含有 **column encryption setting=enabled** ，來連接資料庫並擷取資料。 應用程式預期資料會明確地進行解密。 不過，驅動程式無法解密資料，因為資料不是正確的加密文字。  

## <a name="best-practice"></a>最佳做法  
 
使用指定的使用者帳戶，利用此選項長時間執行工作負載。  
 
針對短時間執行且需要移動加密資料 (而不將其解密) 的大量複製應用程式或工具，在執行應用程式之前，即時將選項設為 ON，並在執行作業之後立即將它設回 OFF。  
 
不要使用此選項來開發新的應用程式。 請改用可提供 API 隱藏單一工作階段之密碼編譯中繼資料檢查的用戶端驅動程式，例如適用於 SQL Server 之 .NET Framework Data Provider 中的 [AllowEncryptedValueModifications] 選項。請參閱 [使用 SqlBulkCopy 複製加密的資料](develop-using-always-encrypted-with-net-framework-data-provider.md#copying-encrypted-data-using-sqlbulkcopy)。 

## <a name="next-steps"></a>後續步驟
- [使用 Always Encrypted 與 SQL Server Management Studio 查詢資料行](always-encrypted-query-columns-ssms.md)
- [使用 Always Encrypted 開發應用程式](always-encrypted-client-development.md)

## <a name="see-also"></a>另請參閱  
- [一律加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [使用 Always Encrypted 與 SQL Server [匯入及匯出精靈]，將資料移轉進或移轉出資料行](always-encrypted-migrate-using-import-export-wizard.md)
- [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
- [ALTER USER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   

