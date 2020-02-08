---
title: 使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: e370af38481593404629fb3367deb3b9f54bb869
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "73595673"
---
# <a name="create-and-use-indexes-on-columns-using-always-encrypted-with-secure-enclaves"></a>使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

本文描述如何在使用已啟用記憶體保護區的金鑰與[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md) 所加密資料行上建立及使用索引。 

具有安全記憶體保護區的 Always Encrypted 支援：
- 使用確定性加密和已啟用記憶體保護區的金鑰所加密資料行上的叢集和非叢集索引。
  - 這類索引會根據加密文字排序。 這類索引沒有特殊考量。 管理和使用這類索引的方式，與使用確定性加密和未啟用記憶體保護區的金鑰在加密資料行上建立索引 (也與 Always Encrypted 相同)。 
- 使用隨機化加密和已啟用記憶體保護區的金鑰在加密資料行上建立非叢集索引。
  - 在記憶體保護區內處理查詢很有用，並可確保使用隨機化加密在加密資料行上建立的索引不會外洩敏感性資料。 索引資料結構 (B 型樹狀結構) 中的索引鍵值會進行加密，並根據其純文字值排序。 如需詳細資訊，請參閱[使用隨機化加密在已啟用記憶體保護區的資料行上建立索引](always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)。

> [!NOTE]
> 本文其餘部分將討論使用隨機化加密和已啟用記憶體保護區的金鑰在加密資料行上建立非叢集索引。

由於使用隨機化加密和已啟用記憶體保護區資料行加密金鑰的資料行上索引包含根據純文字排序的加密 (加密文字) 資料，因此 SQL Server 引擎必須針對涉及建立、更新或搜尋索引的任何作業使用記憶體保護區，包括：

- 建立或重建索引。
- 插入、更新或刪除資料表中的資料列 (包含已編製索引/已加密的資料行)，這會觸發將索引鍵插入索引和/或從索引移除索引鍵。
- 執行涉及檢查索引完整性的 `DBCC` 命令，例如 [DBCC CHECKDB (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 或 [DBCC CHECKTABLE (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)。
- 資料庫復原 (例如在 SQL Server 失敗並重新啟動後)，若 SQL Server 需要復原對索引進行的任何變更 (請參閱以下詳細資料)。

所有上述作業都需要記憶體保護區具備適用於已編製索引之資料行的資料行加密金鑰。 必須有此金鑰才能將索引鍵解密。 一般而言，記憶體保護區可以透過兩種方式取得資料行加密金鑰：
- 直接從用戶端應用程式取得。
- 從資料行加密金鑰的快取取得。

## <a name="invoke-indexing-operations-with-column-encryption-keys-provided-directly-by-the-client"></a>搭配由用戶端直接提供的資料行加密金鑰來叫用編制索引作業
若要讓這個叫用編製索引作業的方法能夠運作，發出會在索引上觸發作業之查詢的應用程式 (包括 SQL Server Management Studio (SSMS) 等工具) 必須：

- 在針對資料庫連接同時啟用 Always Encrypted 及記憶體保護區計算的情況下連接到資料庫。
- 應用程式必須能存取保護已編制索引資料行之資料行加密金鑰的資料行主要金鑰。

在 SQL Server 引擎剖析應用程式查詢，並判斷其必須更新加密資料行上的索引以執行該查詢之後，會指示用戶端驅動程式透過安全通道向記憶體保護區提供必要的資料行加密金鑰。 此機制和用來向記憶體保護區提供資料行加密金鑰以處理所有其他查詢的機制完全相同。 例如，使用模式比對和範圍比較的就地加密或查詢。

此方法很適合用來確保在已啟用 Always Encrypted 和記憶體保護區計算情況下已連接到資料庫的應用程式，能夠對加密資料行上是否有索引一目瞭然。 此應用程式連接可以使用記憶體保護區進行查詢處理。 在您於資料行上建立索引之後，應用程式內的驅動程式將會透明地向記憶體保護區提供資料行加密金鑰，以進行編制索引作業。 請注意，建立索引可能會增加需要應用程式將資料行加密金鑰傳送至記憶體保護區的查詢數目。

若要使用此方法，請遵循[使用具有安全記憶體保護區的 Always Encrypted 查詢資料行](always-encrypted-enclaves-query-columns.md)中有關使用安全記憶體保護區來執行查詢的一般指導方針。

如需如何使用此方法的逐步指示，請參閱[教學課程：使用隨機化加密在已啟用記憶體保護區的資料行上建立及使用索引](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)。

## <a name="invoke-indexing-operations-using-cached-column-encryption-keys"></a>使用已快取的資料行加密金鑰來叫用編制索引作業

在用戶端應用程式將資料行加密金鑰傳送至記憶體保護區，以處理需要記憶體保護區計算的任何查詢之後，記憶體保護區會將資料行加密金鑰快取於內部快取之中。 此快取位於記憶體保護區內，且無法從外部存取。

如果有相同或不同使用者所使用的相同或另一個用戶端應用程式，在沒有直接提供必要資料行加密的情況下於索引上觸發作業，則記憶體保護區將會在快取中查詢資料行加密金鑰。 如此一來，索引上的作業會成功，即便用戶端應用程式沒有提供金鑰。

若要讓這個叫用編制索引作業的方法能夠運作，應用程式必須在沒有針對連線啟用 Always Encrypted 的情況下連線至資料庫，且必要的資料行加密金鑰必須在記憶體保護區內的快取中可供使用。

這個叫用作業的方法僅支援針對其他 (與索引無關的) 作業不需要資料行加密金鑰的查詢。 例如，使用 `INSERT` 陳述式將資料列插入包含加密資料行之資料表的應用程式，必須在連接字串中已啟用 Always Encrypted 的情況下連接到資料庫，且必須能夠存取金鑰，無論加密資料行是否具有索引。

這個方法很適合用來：
 - 確保使用隨機化加密的已啟用記憶體保護區之資料行上的索引，對於無法以純文字存取金鑰和資料的應用程式和使用者來說能夠透明地呈現。 
 - 確保在加密資料行上建立索引不會中斷現有的查詢。 如果應用程式不需要能夠存取金鑰就能在包含加密資料行的資料表上發出查詢，則該應用程式將可以在 DBA 建立索引之後繼續執行，而無須存取金鑰。 例如，假設應用程式在包含加密資料行的 **Employees** 資料表上執行下列查詢。 DBA 尚未在任何加密資料行上建立索引。

   ```sql
   DELETE FROM [dbo].[Employees] WHERE [EmployeeID] = 1;
   GO
   ```

   如果應用程式透過未啟用 Always Encrypted 和記憶體保護區計算的連接提交查詢，查詢將會成功。 該查詢不會在加密資料行上觸發任何計算。 在 DBA 於任何加密資料行上建立索引之後，該查詢會觸發從索引移除索引鍵的動作。 在此情況下，記憶體保護區需要資料行加密金鑰。 不過，應用程式將能繼續透過相同的連線執行此查詢，只要資料擁有者持續將資料行加密金鑰提供給記憶體保護區。

 - 這能在管理索引上達成角色區隔，因為它能讓 DBA 在無法存取敏感性資料的情況下，建立及改變已加密資料行上的索引。 

> [!TIP] 
> [sp_enclave_send_keys (Transact-SQL)](../../system-stored-procedures/sp-enclave-send-keys-sql.md) 可讓您輕鬆地將用於索引之所有已啟用記憶體保護區的資料行加密金鑰傳送到金鑰快取。

如需如何使用此方法的逐步指示，請參閱[教學課程：使用隨機化加密在已啟用記憶體保護區的資料行上建立及使用索引](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)。 

## <a name="next-steps"></a>後續步驟
- [使用具有安全記憶體保護區的 Always Encrypted 查詢資料行](always-encrypted-enclaves-query-columns.md)。

## <a name="see-also"></a>另請參閱  
- [教學課程：使用隨機化加密在已啟用記憶體保護區的資料行上建立及使用索引](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)。
- [sp_enclave_send_keys (Transact-SQL)](../../system-stored-procedures/sp-enclave-send-keys-sql.md)
