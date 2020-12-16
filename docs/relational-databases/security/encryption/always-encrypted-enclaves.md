---
title: 具有安全記憶體保護區的 Always Encrypted
description: 了解適用於 SQL Server 的具有安全記憶體保護區的 Always Encrypted 功能。
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: a3da2dbe104b0a02ef9b973521ef14e5959a832c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480879"
---
# <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]
 
具有安全記憶體保護區的 Always Encrypted 可為 [Always Encrypted](always-encrypted-database-engine.md) 功能提供額外功能。

Always Encrypted 已在 SQL Server 2016 中引進，可保護敏感性資料的機密性，免於遭受惡意程式碼和 SQL Server 高權限的「未經授權」使用者威脅。 高權限的未經授權使用者為 DBA、電腦系統管理員、雲端系統管理員，或是對伺服器執行個體、硬體等具有合法存取權，但不應該具有部分或所有實際資料存取權的其他人。  

若沒有此文章討論的增強功能，Always Encrypted 將透過在用戶端將資料加密來保護資料，並且絕不允許資料或對應的密碼編譯金鑰以純文字形式出現在 SQL Server 引擎內部。 因此，資料庫內部的加密資料行功能受到嚴格限制。 SQL Server 可對加密資料執行相的唯一作業是相等比較 (而且僅適用於確定性加密)。 資料庫內部不支援所有其他作業，包括密碼編譯作業 (初始資料加密或金鑰輪替) 及/或豐富計算 (例如，模式比對)。 使用者需要將資料移出資料庫以在用戶端執行這些作業。

具有安全記憶體保護區的 Always Encrypted 允許在伺服器端的安全記憶體保護區內部進行純文字資料計算，藉以解決這些限制。 安全記憶體保護區是 SQL Server 處理序內受保護的記憶體區域，並可作為受信任的執行環境來處理 SQL Server 引擎內部的敏感性資料。 安全記憶體保護區對於主控電腦上其餘部分的 SQL Server 和其他處理序會顯示為不透明盒子。 即使使用偵錯工具，也沒有辦法從外部檢視記憶體保護區內部的任何資料或程式碼。  


Always Encrypted 會使用安全記憶體保護區，如下圖所示：

![資料流程](./media/always-encrypted-enclaves/ae-data-flow.png)



剖析時應用程式的查詢時，SQL Server 引擎會判斷查詢是否包含任何需要使用安全記憶體保護區的加密資料作業。 針對需要存取安全記憶體保護區的查詢：

- 用戶端驅動程式會將作業所需的資料行加密金鑰傳送至安全記憶體保護區 (透過安全通道)。 
- 接著，用戶端驅動程式會送出要執行的查詢，以及加密的查詢參數。

在查詢處理期間，資料或資料行加密金鑰不會以純文字形式公開在安全記憶體保護區外的 SQL Server 引擎中。 SQL Server 引擎會將密碼編譯作業和加密資料行計算委派給安全記憶體保護區。 若有需要，安全記憶體保護區會解密查詢參數及/或加密資料行中儲存的資料，並執行所要求的作業。

在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中，具有安全記憶體保護區的 Always Encrypted 會使用[虛擬式安全性 (VBS)](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) \(英文\) 來保護 Windows 中的記憶體保護區 (也稱為虛擬安全模式或 VSM 記憶體保護區)。

## <a name="why-use-always-encrypted-with-secure-enclaves"></a>為何要使用具有安全記憶體保護區的 Always Encrypted？

運用安全記憶體保護區，Always Encrypted 可保護敏感性資料的機密性，同時提供下列好處：

- **就地加密** - 敏感性資料的密碼編譯作業 (例如：初始資料加密或輪替資料行加密金鑰) 會在安全記憶體保護區內執行，而不需要將資料移出資料庫。 您可以使用 ALTER TABLE Transact-SQL 陳述式來發出就地加密，而不需要使用 SSMS 中的 [Always Encrypted 精靈] 或 Set-SqlColumnEncryption PowerShell Cmdlet 等工具。

- **豐富計算** - 安全記憶體保護區內支援加密資料行作業，包括模式比對 (LIKE 述詞) 及範圍比較，這可為需要在資料庫系統內執行這類計算的各種應用程式和案例解除鎖定 Always Encrypted 功能。

## <a name="secure-enclave-attestation"></a>安全記憶體保護區證明

SQL Server 引擎內部的安全記憶體保護區能夠以純文字形式存取加密資料庫資料行中儲存的敏感性資料與對應的資料行加密金鑰。 將涉及記憶體保護區計算的查詢提交給 SQL Server 之前，應用程式內部的用戶端驅動程式必須確認安全記憶體保護區是根據指定技術 (例如 VBS) 的真正記憶體保護區，而且已簽署在記憶體保護區內部執行的程式碼，以便在記憶體保護區內部執行。 

驗證記憶體保護區的處理序稱為 **記憶體保護區證明**，它會同時涉及應用程式內的用戶端驅動程式，以及與外部證明服務連絡的 SQL Server。 證明處理序的細節取決於記憶體保護區技術和證明服務。

SQL Server 在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中支援 VBS 安全記憶體保護區的證明處理序是 Windows Defender 系統防護執行階段證明，它會使用主機守護者服務 (HGS) 作為證明服務。 您需要在環境中設定 HGS，並在 HGS 中註冊裝載 SQL Server 執行個體的電腦。 您還必須使用 HGS 證明來設定用戶端應用程式或工具 (例如 SQL Server Management Studio)。

## <a name="supported-client-drivers"></a>支援的用戶端驅動程式

若要使用具有安全記憶體保護區的 Always Encrypted，應用程式必須使用支援此功能的用戶端驅動程式。 您必須設定應用程式和用戶端驅動程式，以啟用記憶體保護區計算和記憶體保護區證明。 如需詳細資料 (包括支援的用戶端驅動程式清單)，請參閱[使用 Always Encrypted 開發應用程式](always-encrypted-client-development.md)。

## <a name="enclave-enabled-keys"></a>已啟用記憶體保護區的金鑰

具有安全記憶體保護區的 Always Encrypted 引入了已啟用記憶體保護區的金鑰概念：

- **已啟用記憶體保護區的資料行主要金鑰** - 在資料庫內部資料行主要金鑰中繼資料物件中已指定 ENCLAVE_COMPUTATIONS 屬性的資料行主要金鑰。 資料行主要金鑰中繼資料物件也必須包含中繼資料屬性的有效簽章。
- **已啟用記憶體保護區的資料行加密金鑰** - 以已啟用記憶體保護區的資料行主要金鑰進行加密的資料行加密金鑰。

當 SQL Server 引擎判斷查詢中指定的作業需要在安全記憶體保護區內部執行時，SQL Server 引擎會要求用戶端驅動程式共用使用安全記憶體保護區進行計算所需的資料行加密金鑰。 只有在金鑰已啟用記憶體保護區 (意即以已啟用記憶體保護區的資料行主要金鑰進行加密)，並已正確簽署時，用戶端驅動程式才會共用資料行加密金鑰。 否則，此查詢會失敗。

如需詳細資訊，請參閱[為具有安全記憶體保護區的 Always Encrypted 管理金鑰](always-encrypted-enclaves-manage-keys.md)。

## <a name="enclave-enabled-columns"></a>已啟用記憶體保護區的資料行

已啟用記憶體保護區的資料行是以已啟用記憶體保護區資料行加密金鑰進行加密的資料庫資料行。 已啟用記憶體保護區資料行可使用的功能取決於資料行所使用加密類型。

- **確定性加密** - 已啟用記憶體保護區的資料行若使用確定性加密，就能在安全記憶體保護區內部支援就地加密，但不支援任何其他作業。 相等比較雖然受到支援，但它會透過在記憶體保護區外部比較加密文字來執行。  
- **隨機化加密** - 已啟用記憶體保護區的資料行若使用隨機化加密，就能在安全記憶體保護區內部支援就地加密及豐富計算。 支援的豐富計算是模式比對和[比較運算子](../../../t-sql/language-elements/comparison-operators-transact-sql.md)，包括相等比較。

如需加密類型的詳細資訊，請參閱 [Always Encrypted 密碼編譯](always-encrypted-cryptography.md)。

下表摘要說明可用於加密資料行的功能，這取決於資料行是否使用已啟用記憶體保護區的資料行加密金鑰和加密類型。

| **運算**| **資料行不是已啟用記憶體保護區的資料行** |**資料行不是已啟用記憶體保護區的資料行**| **資料行是已啟用記憶體保護區的資料行**  |**資料行是已啟用記憶體保護區的資料行** |
|:---|:---|:---|:---|:---|
| | **隨機化加密**  | **確定性加密**     | **隨機化加密**      | **確定性加密**     |
| **就地加密** | 不支援  | 不支援   | 支援         | 支援    |
| **相等比較**   | 不支援 | 支援記憶體保護區外部 | 支援 (記憶體保護區內部) | 支援記憶體保護區外部 |
| **超出相等的比較運算子** | 不支援  | 不支援   | 支援      | 不支援     |
| **LIKE**    | 不支援      | 不支援    | 支援     | 不支援    |

就地加密包含對下列記憶體保護區內部作業的支援：

- 初始加密現有資料行中儲存的資料。
- 重新加密資料行中的現有資料，例如：
  
  - 輪替資料行加密金鑰 (使用新的金鑰重新加密資料行)。
  - 變更加密類型。  

- 解密加密資料行中儲存的資料 (將資料行轉換成純文字資料行)。

為了能夠進行就地加密，密碼編譯作業所涉及的資料行加密金鑰必須是已啟用記憶體保護區的金鑰：

- 初始加密：所要加密資料行的資料行加密金鑰必須是已啟用記憶體保護區的金鑰。
- 重新加密：目前和目標資料行加密金鑰 (如果不同於目前的金鑰) 都必須是已啟用記憶體保護區的金鑰。
- 解密：資料行的目前資料行加密金鑰必須為已啟用記憶體保護區。

### <a name="indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>使用隨機加密啟用記憶體保護區資料行上的索引
您可以在使用隨機加密啟用記憶體保護區的資料行上建立非叢集索引，使豐富查詢速度更快。 為了確保使用隨機加密進行加密資料行上的索引不會外洩敏感性資料，並且在同時確保能夠針對在記憶體保護區內部處理的查詢發揮用途，索引資料結構 (B 型樹狀結構) 中的索引鍵值會進行加密，並根據其純文字的值排序。 當 SQL Server 引擎中的查詢執行程式使用加密資料行上的索引，於記憶體保護區內部進行計算時，它會搜尋索引來尋找儲存在資料行中的特定值。 每個搜尋都可能會涉及多次比較。 查詢執行程式會將每一次的比較委派給記憶體保護區，記憶體保護區則會解密儲存在資料行中的值，以及要比較的加密索引鍵值；它接著會在純文字上執行比較，然後將比較的結果傳回執行程式。 

目前仍不支援在使用隨機加密，但沒有啟用記憶體保護區的資料行上建立索引。

如需詳細資訊，請參閱[使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引](always-encrypted-enclaves-create-use-indexes.md)。 如需 SQL Server 中編製索引方式的一般資訊 (而非 Always Encrypted 特定的資訊)，請參閱[叢集與非叢集索引說明](../../indexes/clustered-and-nonclustered-indexes-described.md)。

#### <a name="database-recovery"></a>資料庫復原

若 SQL Server 的執行個體失敗，其資料庫可能會處於資料檔案仍包含交易中修改項目未完成的狀態。 執行個體啟動時，它會執行稱為[資料庫復原](../../logs/the-transaction-log-sql-server.md#recovery-of-all-incomplete-transactions-when--is-started)的處理序，該處理序會涉及復原交易記錄中所找到的每個未完成交易，確保資料庫的完整性能獲得保留。 若未完成的交易更動了索引，那些變更也必須要復原。 例如，索引中的某些索引鍵值可能需要移除或重新插入。

> [!IMPORTANT]
> Microsoft 強烈建議先為您的資料庫啟用 [高速資料庫復原 (ADR)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr)，**再** 使用隨機加密進行加密，以在啟用記憶體保護區的資料行上建立第一個索引。

若透過[傳統式資料庫復原處理序](/azure/sql-database/sql-database-accelerated-database-recovery#the-current-database-recovery-process) (遵循 [ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf)) 復原對索引進行的變更，SQL Server 必須等待應用程式將資料行的資料行加密金鑰提供給記憶體保護區，這可能會花費很長的時間。 ADR 可大幅減少因為無法在記憶體保護區內的快取中取得資料行加密金鑰，而需延遲的復原作業數。 因此，它可以透過將封鎖新交易的機會降至最低，來大幅增加資料庫的可用性。 啟用 ADR 後，雖然 SQL Server 仍需要資料行加密金鑰來完成清理舊的資料版本，但它會以背景工作的形式進行，不會影響資料庫的可用性或使用者交易。 但是，您仍然可能會在錯誤記錄中看到錯誤訊息，指出因缺少資料行加密金鑰而無法完成清理作業。

### <a name="indexes-on-enclave-enabled-columns-using-deterministic-encryption"></a>使用決定性加密啟用記憶體保護區資料行上的索引

使用決定性加密資料行上的索引會根據加密文字 (而非純文字) 排序，無論資料行是否已啟用記憶體保護區。

## <a name="security-considerations"></a>安全性考量

下列安全性考量事項適用於具備安全記憶體保護區的 Always Encrypted。

- 您記憶體保護區中資料的安全性取決於證明通訊協定和證明服務。 因此，您必須確保證明服務及證明服務強制執行的證明原則，都是由信任的管理員管理。 此外，證明服務通常支援不同的原則和證明通訊協定，其中有些只會執行最小的記憶體保護區及環境驗證，並且旨在用於測試及開發。 請仔細遵循您證明服務的指導方針，確保您針對生產部署使用建議的設定和原則。 
- 搭配啟用記憶體保護區的 CEK 使用隨機加密來加密資料行，可能會外洩儲存在資料行中資料的順序，因為這類資料行支援範圍比較。 例如，若包含員工薪資的加密資料行中具備索引，惡意 VBA 便可以掃描索引來尋找最大的加密薪資值，並識別薪資最高的人員 (假設人員的名稱未加密的話)。 
- 若您使用 Always Encrypted 來保護敏感性資料，使其不受未獲授權的 DBA 存取，請不要與 DBA 共用資料行主要金鑰或資料行加密金鑰。 DBA 可以透過利用記憶體保護區內的資料行加密金鑰快取，在無須直接存取金鑰的情況下管理加密資料行上的索引。

## <a name="considerations-for-availability-groups-and-database-migration"></a><a name="anchorname-1-considerations-availability-groups-db-migration"></a> 可用性群組和資料庫移轉的考量事項

設定支援使用記憶體保護區進行查詢所需要的 Always On 可用性群組時，您需要確保所有裝載可用性群組中資料庫的 SQL Server 執行個體都支援使用安全記憶體保護區的 Always Encrypted 功能，並已設定記憶體保護區。 若主要資料庫支援記憶體保護區，但次要複本不支援，任何嘗試搭配安全記憶體保護區使用 Always Encrypted 功能的查詢都會失敗。

當您還原搭配安全記憶體保護區使用 Always Encrypted 功能的資料庫備份檔案，而該 SQL Server 執行個體並未設定記憶體保護區時，還原作業將會成功，並且所有不依賴記憶體保護區的功能都會開放使用。 但是，後續任何使用記憶體保護區功能的查詢都會失敗，且使用隨機加密啟用記憶體保護區資料行上的索引都會失效。 相同的情況也會在您將搭配安全記憶體保護區使用 Always Encrypted 的資料庫附加到並未設定記憶體保護區的執行個體上發生。

若您資料庫包含使用隨機加密啟用記憶體保護區資料行上的索引，請務必在資料庫中先啟用[高速資料庫復原 (ADR)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr)，再建立資料庫備份。 ADR 將會確保資料庫 (包含索引) 在還原資料庫後立即開放使用。 如需詳細資訊，請參閱[資料庫復原](#database-recovery)。

當您使用 bacpac 檔案遷移資料庫時，您需要確保在建立 bacpac 檔案前，您已卸除所有使用隨機加密啟用索引記憶體保護區的資料行。

## <a name="known-limitations"></a>已知限制
具有安全記憶體保護區的 Always Encrypted 會藉由啟用下列作業來解決 Always Encrypted 的一些限制：

- 就地密碼編譯作業。
- 在使用隨機加密進行加密的資料行上使用模式比對 (LIKE) 和比較運作子。
    > [!NOTE]
    > 目前針對使用 binary2 排序次序 (BIN2 定序) 來定序的字元字串資料行支援以上作業。 使用非 BIN2 定序的字元字串資料行，可使用隨機加密和啟用記憶體保護區的資料行加密金鑰來進行加密。 不過，針對這類資料行所啟用的唯一新功能就是就地加密。
- 使用隨機加密在資料行上建立非叢集索引和統計資料。

[功能詳細資料](always-encrypted-database-engine.md#feature-details)所列出之 Always Encrypted 的所有其他限制，也適用於具有安全記憶體保護區的 Always Encrypted。

下列限制僅適用於具備安全記憶體保護區的 Always Encrypted：

- 無法在使用隨機加密啟用記憶體保護區的資料行上建立叢集索引。
- 使用隨機加密啟用記憶體保護區的資料行不能作為主索引鍵資料行，且無法由外部索引鍵條件約束或唯一索引鍵條件約束參考。
- 在已啟用記憶體保護區 (使用隨機化加密) 的資料行上，僅支援巢狀迴圈聯結 (使用索引，如果有的話)。 不支援雜湊聯結和合併聯結。 
- 除了變更相同字碼頁中的定序和可 NULL 性外，就地密碼編譯作業無法與資料行中繼資料的任何其它變更合併。 例如，您無法加密、重新加密或解密資料行，同時在單一 `ALTER TABLE`/`ALTER COLUMN` Transact-SQL 陳述式中變更資料行的資料類型。 請使用兩個個別的陳述式。
- 不支援對記憶體內部資料表中的資料行使用已啟用記憶體保護區的金鑰。
- 定義計算資料行的運算式，無法使用隨機化加密，在具備記憶體保護區功能的資料行上，執行任何計算 (即使是類似 LIKE 及範圍比較等計算皆無法)。
- 在已啟用記憶體保護區 (使用隨機化加密) 的資料行上，LIKE 運算子的參數中不支援逸出字元。
- 透過使用 LIKE 運算子或具有使用下列任一資料類型 (在加密之後會成為大型物件) 查詢參數的比較運算子所進行的查詢會忽略索引，並執行資料表掃描。
    - `nchar[n]` 和 `nvarchar[n]`，如果 n 大於 3967。
    - `char[n]`、`varchar[n]`、`binary[n]`、`varbinary[n]`，如果 n 大於 7935。
- 工具限制：
  - 若要儲存已啟用記憶體保護區的資料行主要金鑰，唯一支援的金鑰存放區是 Windows 憑證存放區和 Azure Key Vault。
  - 不支援匯入/匯出包含已啟用記憶體保護區金鑰的資料庫。
  - 若要透過 `ALTER TABLE`/`ALTER COLUMN` 觸發就地密碼編譯作業，您必須使用 SSMS 中的查詢視窗發出陳述式，也可以撰寫自己的程式來發出陳述式。 目前，SqlServer PowerShell 模組中的 Set-SqlColumnEncryption Cmdlet 和 SQL Server Management Studio 中的 [Always Encrypted 精靈] 尚未支援就地加密，即使用於作業之資料行加密金鑰是已啟用記憶體保護區的金鑰，但它們會將資料移出資料庫以進行密碼編譯作業。

## <a name="next-steps"></a>後續步驟
- [教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [設定和使用具有安全記憶體保護區的 Always Encrypted](configure-always-encrypted-enclaves.md)

## <a name="see-also"></a>另請參閱
- [為具有安全記憶體保護區的 Always Encrypted 管理金鑰](always-encrypted-enclaves-manage-keys.md)
- [使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密](always-encrypted-enclaves-configure-encryption.md)
- [使用具有安全記憶體保護區的 Always Encrypted 查詢資料行](always-encrypted-enclaves-query-columns.md)
- [為現有加密資料行啟用具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引](always-encrypted-enclaves-create-use-indexes.md)
