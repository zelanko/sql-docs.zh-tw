---
title: 具有安全記憶體保護區的 Always Encrypted (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 22570f7ae8a9f11b89f11027698c948be5766d25
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661220"
---
# <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

 
具有安全記憶體保護區的 Always Encrypted 可為 [Always Encrypted](always-encrypted-database-engine.md) 功能提供額外功能。

Always Encrypted 已在 SQL Server 2016 中引進，可保護敏感性資料的機密性，免於遭受惡意程式碼和 SQL Server 高權限的「未經授權」  使用者威脅。 高權限的未經授權使用者為 DBA、電腦系統管理員、雲端系統管理員，或是對伺服器執行個體、硬體等具有合法存取權，但不應該具有部分或所有實際資料存取權的其他人。 

到目前為止，Always Encrypted 會透過下列方式保護資料：在用戶端將其加密，並且絕不允許資料或對應的密碼編譯金鑰以純文字形式出現在 SQL Server 引擎內部。 因此，資料庫內部的加密資料行功能受到嚴格限制。 SQL Server 可對加密資料執行相的唯一作業是相等比較 (而且相等比較僅適用於確定性加密)。 資料庫內部不支援所有其他作業，包括密碼編譯作業 (初始資料加密或金鑰輪替) 或豐富計算 (例如，模式比對)。 使用者需要將資料移出資料庫以在用戶端執行這些作業。

具有安全記憶體保護區的  Always Encrypted 允許在伺服器端的安全記憶體保護區內部進行純文字資料計算，藉以解決這些限制。 安全記憶體保護區是 SQL Server 處理序內受保護的記憶體區域，並可作為受信任的執行環境來處理 SQL Server 引擎內部的敏感性資料。 安全記憶體保護區對於主控電腦上其餘部分的 SQL Server 和其他處理序會顯示為黑盒子。 即使使用偵錯工具，也沒有辦法從外部檢視記憶體保護區內部的任何資料或程式碼。  


Always Encrypted 會使用安全記憶體保護區，如下圖所示：

![資料流程](./media/always-encrypted-enclaves/ae-data-flow.png)



剖析時應用程式的查詢時，SQL Server 引擎會判斷查詢是否包含任何需要使用安全記憶體保護區的加密資料作業。 針對需要存取安全記憶體保護區的查詢：

- 用戶端驅動程式會將作業所需的資料行加密金鑰傳送至安全記憶體保護區 (透過安全通道)。 
- 接著，用戶端驅動程式會送出要執行的查詢，以及加密的查詢參數。

在查詢處理期間，資料或資料行加密金鑰不會以純文字形式公開在安全記憶體保護區外的 SQL Server 引擎中。 SQL Server 引擎會將密碼編譯作業和加密資料行計算委派給安全記憶體保護區。 若有需要，安全記憶體保護區會解密查詢參數及/或加密資料行中儲存的資料，並執行所要求的作業。

## <a name="why-use-always-encrypted-with-secure-enclaves"></a>為何要使用具有安全記憶體保護區的 Always Encrypted？

運用安全記憶體保護區，Always Encrypted 可保護敏感性資料的機密性，同時提供下列好處：

- **就地加密** - 敏感性資料的密碼編譯作業 (例如：初始資料加密或輪替資料行加密金鑰) 會在安全記憶體保護區內執行，而不需要將資料移出資料庫。 您可以使用 ALTER TABLE Transact-SQL 陳述式來發出就地加密，而不需要使用 SSMS 中的 [Always Encrypted 精靈] 或 Set-SqlColumnEncryption PowerShell Cmdlet 等工具。

- **豐富計算 (預覽)** - 安全記憶體保護區內支援加密資料行作業，包括模式比對 (LIKE 述詞) 及範圍比較，這可為需要在資料庫系統內執行這類計算的各種應用程式和案例解除鎖定 Always Encrypted 功能。

> [!IMPORTANT]
> 在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中，豐富計算功能會導致效能最佳化及錯誤處理增強功能暫止，因此目前根據預設會停用此功能。 若要啟用豐富計算，請參閱[啟用豐富計算](configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中，具有安全記憶體保護區的 Always Encrypted 會使用[虛擬式安全性 (VBS)](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) \(英文\) 來保護 Windows 中的記憶體保護區 (也稱為虛擬安全模式或 VSM 記憶體保護區)。

## <a name="secure-enclave-attestation"></a>安全記憶體保護區證明

SQL Server 引擎內部的安全記憶體保護區能夠以純文字形式存取加密資料庫資料行中儲存的敏感性資料與對應的資料行加密金鑰。 將涉及記憶體保護區計算的查詢提交給 SQL Server 之前，應用程式內部的用戶端驅動程式必須確認安全記憶體保護區是根據指定技術 (例如 VBS) 的真正記憶體保護區，而且已簽署在記憶體保護區內部執行的程式碼，以便在記憶體保護區內部執行。 

驗證記憶體保護區的處理序稱為**記憶體保護區證明**，它通常會同時涉及應用程式內的用戶端驅動程式，以及與外部證明服務連絡的 SQL Server。 證明處理序的細節取決於記憶體保護區技術和證明服務。

SQL Server 在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中支援 VBS 安全記憶體保護區的證明處理序是 Windows Defender 系統防護執行階段證明，它會使用主機守護者服務 (HGS) 作為證明服務。 您需要在環境中設定 HGS，並在 HGS 中註冊裝載 SQL Server 執行個體的電腦。 您還必須使用 HGS 證明來設定用戶端應用程式或工具 (例如 SQL Server Management Studio)。

## <a name="secure-enclave-providers"></a>安全記憶體保護區提供者

若要使用具有安全記憶體保護區的 Always Encrypted，應用程式必須使用支援此功能的用戶端驅動程式。 在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中，您的應用程式必須使用 .NET Framework 4.7.2 和 .NET Framework Data Provider for SQL Server。 此外，.NET 應用程式還必須設有記憶體保護區類型 (例如 VBS) 專用的 **安全記憶體保護區提供者**，以及您要使用的證明服務 (例如 HGS)。 支援的記憶體保護區提供者隨附於個別 NuGet 套件，您必須將其與您的應用程式整合。 記憶體保護區提供者會實作用戶端邏輯，用於證明通訊協定以及與指定類型的記憶體保護區建立安全通道。

## <a name="enclave-enabled-keys"></a>已啟用記憶體保護區的金鑰

具有安全記憶體保護區的 Always Encrypted 引入了已啟用記憶體保護區的金鑰概念：

- **已啟用記憶體保護區的資料行主要金鑰** - 在資料庫內部資料行主要金鑰中繼資料物件中已指定 ENCLAVE_COMPUTATIONS 屬性的資料行主要金鑰。 資料行主要金鑰中繼資料物件也必須包含中繼資料屬性的有效簽章。
- **已啟用記憶體保護區的資料行加密金鑰** - 以已啟用記憶體保護區的資料行主要金鑰進行加密的資料行加密金鑰。

當 SQL Server 引擎判斷查詢中指定的作業需要在安全記憶體保護區內部執行時，SQL Server 引擎會要求用戶端驅動程式共用使用安全記憶體保護區進行計算所需的資料行加密金鑰。 只有在金鑰已啟用記憶體保護區 (意即以已啟用記憶體保護區的資料行主要金鑰進行加密)，並已正確簽署時，用戶端驅動程式才會共用資料行加密金鑰。 否則，此查詢會失敗。

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
您可以在使用隨機加密啟用記憶體保護區的資料行上建立非叢集索引，使豐富查詢速度更快。 為了確保使用隨機加密進行加密資料行上的索引不會外洩敏感性資料，並且在同時確保能夠針對在記憶體保護區內部處理的查詢發揮用途，索引資料結構 (B 型樹狀結構) 中的索引鍵值會進行加密，並根據其純文字的值排序。 當 SQL Server 引擎中的查詢執行程式使用加密資料行上的索引，於記憶體保護區內部進行計算時，它會搜尋索引來尋找儲存在資料行中的特定值。 每個搜尋都可能會涉及多次比較。 查詢執行程式會將每一次的比較委派給記憶體保護區，記憶體保護區則會解密儲存在資料行中的值，以及要比較的加密索引鍵值；它接著會在純文字上執行比較，然後將比較的結果傳回執行程式。 如需 SQL Server 中編製索引方式的一般資訊 (而非 Always Encrypted 特定的資訊)，請參閱[叢集與非叢集索引說明](../../indexes/clustered-and-nonclustered-indexes-described.md)。

因為使用隨機加密啟用記憶體保護區資料行上的索引會儲存加密的索引鍵值，同時值本身會根據純文字進行排序，SQL Server 引擎必須針對任何涉及建立或更新索引的作業使用記憶體保護區，包括：
- 建立或重建索引。
- 插入、更新或刪除資料表中的資料列 (包含已編製索引/已加密的資料行)，這些行為會觸發針對索引將索引鍵插入或/和移除的動作。
- 執行涉及檢查索引完整性的 DBCC 命令，例如 [DBCC CHECKDB (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 或 [DBCC CHECKTABLE (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)。
- 資料庫復原 (例如在 SQL Server 失敗並重新啟動後)，若 SQL Server 需要復原對索引進行的任何變更 (請參閱下方的詳細資料)。

所有上述的作業都需要記憶體保護區具備適用於已編制索引之資料行的資料行加密金鑰，才能解密索引鍵。 一般而言，記憶體保護區可以透過兩種方式取得資料行加密金鑰：

- **直接從在索引上叫用作業的用戶端應用程式取得**，如以上簡介所說明。 此方法需要應用程式或使用者擁有資料行主要金鑰的存取權限，以及保護索引資料行的資料行加密金鑰存取權限。 應用程式必須連線到針對連線啟用 Always Encrypted 的資料庫。
- **從資料行加密金鑰的快取取得。** 記憶體保護區會在快取中儲存先前查詢所使用的金鑰，由於該快取位於記憶體保護區內部，因此無法從外部存取。 若應用程式在索引上觸發作業，卻沒有直接提供必要的資料行加密金鑰，記憶體保護區便會在快取中尋找金鑰。 若記憶體保護區在快取中找到金鑰，便會用於作業。 此方法可讓 DBA 管理索引，並執行特定的資料清理作業 (例如從包含加密資料行上索引的資料表中移除資料列)，而無須存取密碼編譯金鑰或純文字格式的資料。 此方法需要應用程式連線到未針對連線啟用 Always Encrypted 的資料庫。

目前仍不支援在使用隨機加密，但沒有啟用記憶體保護區的資料行上建立索引。

#### <a name="database-recovery"></a>資料庫復原

若 SQL Server 的執行個體失敗，其資料庫可能會處於資料檔案仍包含交易中修改項目未完成的狀態。 執行個體啟動時，它會執行稱為[資料庫復原](../../logs/the-transaction-log-sql-server.md#recovery-of-all-incomplete-transactions-when--is-started)的處理序，該處理序會涉及復原交易記錄中所找到的每個未完成交易，確保資料庫的完整性能獲得保留。 若未完成的交易更動了索引，那些變更也必須要復原。 例如，索引中的某些索引鍵值可能需要移除或重新插入。

> [!IMPORTANT]
> Microsoft 強烈建議先為您的資料庫啟用[高速資料庫復原 (ADR)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr)，**再**使用隨機加密進行加密，以在啟用記憶體保護區的資料行上建立第一個索引。

若透過[傳統式資料庫復原處理序](https://docs.microsoft.com/azure/sql-database/sql-database-accelerated-database-recovery#the-current-database-recovery-process) (遵循 [ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf)) 復原對索引進行的變更，SQL Server 必須等待應用程式將資料行的資料行加密金鑰提供給記憶體保護區，這可能會花費很長的時間。 ADR 可大幅減少因為無法在記憶體保護區內的快取中取得資料行加密金鑰，而需延遲的復原作業數。 因此，它可以透過將封鎖新交易的機會降至最低，來大幅增加資料庫的可用性。 啟用 ADR 後，雖然 SQL Server 仍需要資料行加密金鑰來完成清理舊的資料版本，但它會以背景工作的形式進行，不會影響資料庫的可用性或使用者交易。 但是，您仍然可能會在錯誤記錄中看到錯誤訊息，指出因缺少資料行加密金鑰而無法完成清理作業。

### <a name="indexes-on-enclave-enabled-columns-using-deterministic-encryption"></a>使用決定性加密啟用記憶體保護區資料行上的索引

使用決定性加密資料行上的索引會根據加密文字 (而非純文字) 排序，無論資料行是否已啟用記憶體保護區。

## <a name="security-considerations"></a>安全性考量

下列安全性考量事項適用於具備安全記憶體保護區的 Always Encrypted。

- 您記憶體保護區中資料的安全性取決於證明通訊協定和證明服務。 因此，您必須確保證明服務及證明服務強制執行的證明原則，都是由信任的管理員管理。 此外，證明服務通常支援不同的原則和證明通訊協定，其中有些只會執行最小的記憶體保護區及環境驗證，並且旨在用於測試及開發。 請仔細遵循您證明服務的指導方針，確保您針對生產部署使用建議的設定和原則。 
- 搭配啟用記憶體保護區的 CEK 使用隨機加密來加密資料行，可能會外洩儲存在資料行中資料的順序，因為這類資料行支援範圍比較。 例如，若包含員工薪資的加密資料行中具備索引，惡意 VBA 便可以掃描索引來尋找最大的加密薪資值，並識別薪資最高的人員 (假設人員的名稱未加密的話)。 
- 若您使用 Always Encrypted 來保護敏感性資料，使其不受未獲授權的 DBA 存取，請不要與 DBA 共用資料行主要金鑰或資料行加密金鑰。 DBA 可以透過利用記憶體保護區內的資料行加密金鑰快取，在無須直接存取金鑰的情況下管理加密資料行上的索引。

## <a name="anchorname-1-considerations-availability-groups-db-migration"></a> 可用性群組和資料庫移轉的考量事項

設定支援使用記憶體保護區進行查詢所需要的 Always On 可用性群組時，您需要確保所有裝載可用性群組中資料庫的 SQL Server 執行個體都支援使用安全記憶體保護區的 Always Encrypted 功能，並已設定記憶體保護區。 若主要資料庫支援記憶體保護區，但次要複本不支援，任何嘗試搭配安全記憶體保護區使用 Always Encrypted 功能的查詢都會失敗。

當您還原搭配安全記憶體保護區使用 Always Encrypted 功能的資料庫備份檔案，而該 SQL Server 執行個體並未設定記憶體保護區時，還原作業將會成功，並且所有不依賴記憶體保護區的功能都會開放使用。 但是，後續任何使用記憶體保護區功能的查詢都會失敗，且使用隨機加密啟用記憶體保護區資料行上的索引都會失效。 相同的情況也會在您將搭配安全記憶體保護區使用 Always Encrypted 的資料庫附加到並未設定記憶體保護區的執行個體上發生。

若您資料庫包含使用隨機加密啟用記憶體保護區資料行上的索引，請務必在資料庫中先啟用[高速資料庫復原 (ADR)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr)，再建立資料庫備份。 ADR 將會確保資料庫 (包含索引) 在還原資料庫後立即開放使用。 如需詳細資訊，請參閱[資料庫復原](#database-recovery)。

當您使用 bacpac 檔案遷移資料庫時，您需要確保在建立 bacpac 檔案前，您已卸除所有使用隨機加密啟用索引記憶體保護區的資料行。

## <a name="known-limitations"></a>已知限制

安全記憶體保護區會強化 Always Encrypted 的功能。 目前針對**啟用記憶體保護區的資料行支援**下列功能：

- 就地密碼編譯作業。
- 在使用隨機加密進行加密的資料行上使用模式比對 (LIKE) 和比較運作子。
    > [!NOTE]
    > 目前針對使用 binary2 排序次序 (BIN2 定序) 來定序的字元字串資料行支援以上作業。 使用非 BIN2 定序的字元字串資料行，可使用隨機加密和啟用記憶體保護區的資料行加密金鑰來進行加密。 不過，針對這類資料行所啟用的唯一新功能就是就地加密。
- 使用隨機加密在資料行上建立非叢集索引。
- 使用包含 LIKE 述詞運算式的計算資料行和使用隨機加密資料行上的比較運算子。

所有其它在[功能詳細資料](always-encrypted-database-engine.md#feature-details)中針對 Always Encrypted (沒有安全記憶體保護區) 所列出的限制 (並未由以上加強內容處理的項目) 也都適用於具備安全記憶體保護區的 Always Encrypted。

下列限制僅適用於具備安全記憶體保護區的 Always Encrypted：

- 無法在使用隨機加密啟用記憶體保護區的資料行上建立叢集索引。
- 使用隨機加密啟用記憶體保護區的資料行不能作為主索引鍵資料行，且無法由外部索引鍵條件約束或唯一索引鍵條件約束參考。
- 不支援在使用隨機加密啟用記憶體保護區的資料行上進行雜湊聯結和合併聯結。 只支援巢狀迴圈聯結 (如果可用的話，使用索引)。
- 透過使用 LIKE 運算子或具有使用下列任一資料類型 (在加密之後會成為大型物件) 查詢參數的比較運算子所進行的查詢會忽略索引，並執行資料表掃描。
    - nchar[n] 及 nvarchar[n]，若 n 大於 3967。
    - char[n]、varchar[n]、binary[n]、varbinary[n]，若 n 大於 7935。
- 除了變更相同字碼頁中的定序和可 NULL 性外，就地密碼編譯作業無法與資料行中繼資料的任何其它變更合併。 例如，您無法加密、重新加密或解密資料行，同時在單一 ALTER TABLE 或 ALTER COLUMN Transact-SQL 陳述式中變更資料行的資料類型。 請使用兩個個別的陳述式。
- 不支援對記憶體內部資料表中的資料行使用已啟用記憶體保護區的金鑰。
- 若要儲存已啟用記憶體保護區的資料行主要金鑰，唯一支援的金鑰存放區是 Windows 憑證存放區和 Azure Key Vault。

下列限制適用於 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]，但已納入要解決的藍圖中：

- 不支援為使用隨機加密啟用記憶體保護區的資料行建立統計資料。
- 針對具有安全記憶體保護區的 Always Encrypted，唯一支援此功能的用戶端驅動程式是 .NET Framework 4.7.2 中的 .NET Framework Data Provider for SQL Server (ADO.NET)。 不支援 ODBC/JDBC。
- 針對具有安全記憶體保護區的 Always Encrypted，目前的工具支援並不完整。 尤其是：
  - 不支援匯入/匯出包含已啟用記憶體保護區金鑰的資料庫。
  - 若要透過 ALTER TABLE Transact-SQL 陳述式觸發就地密碼編譯作業，您必須使用 SSMS 中的查詢視窗發出陳述式，也可以撰寫自己的程式來發出陳述式。 SqlServer PowerShell 模組中的 Set-SqlColumnEncryption Cmdlet 和 SQL Server Management Studio 中的 [Always Encrypted 精靈] 尚未支援就地加密，即使用於作業之資料行加密金鑰是已啟用記憶體保護區的金鑰，但這兩個工具目前會將資料移出資料庫以進行密碼編譯作業。
- 不支援檢查索引完整性或更新索引的 DBCC 命令。
- 在建立資料表 (透過 CREATE TABLE) 的同時在加密資料行上建立索引。 您需要透過 CREATE INDEX 分別在加密資料行上建立索引。

## <a name="next-steps"></a>後續步驟

- 設定測試環境並在 SSMS 中嘗試具有安全記憶體保護區的 Always Encrypted 功能，請參閱[教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)。
- 如需如何搭配安全記憶體保護區使用 Always Encrypted 的詳細資料，請參閱[使用安全記憶體保護區設定 Always Encrypted](configure-always-encrypted-enclaves.md)。
