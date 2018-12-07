---
title: 具有安全記憶體保護區的 Always Encrypted (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 9dfc5e2cf7bab164d650f2da1767b2a0e7c399aa
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2018
ms.locfileid: "52711179"
---
# <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]


具有安全記憶體保護區的 Always Encrypted 可為 [Always Encrypted](always-encrypted-database-engine.md) 功能提供額外功能。

Always Encrypted 已在 SQL Server 2016 中引進，可保護敏感性資料的機密性，免於遭受惡意程式碼和 SQL Server 高權限的「未經授權」使用者威脅。 高權限的未經授權使用者為 DBA、電腦系統管理員、雲端系統管理員，或是對伺服器執行個體、硬體等具有合法存取權，但不應該具有部分或所有實際資料存取權的其他人。 

到目前為止，Always Encrypted 會透過下列方式保護資料：在用戶端將其加密，並且絕不允許資料或對應的密碼編譯金鑰以純文字形式出現在 SQL Server 引擎內部。 因此，資料庫內部的加密資料行功能受到嚴格限制。 SQL Server 可對加密資料執行相的唯一作業是相等比較 (而且相等比較僅適用於確定性加密)。 資料庫內部不支援所有其他作業，包括密碼編譯作業 (初始資料加密或金鑰輪替) 或豐富計算 (例如，模式比對)。 使用者需要將資料移出資料庫以在用戶端執行這些作業。

具有安全記憶體保護區的 Always Encrypted 允許在伺服器端的安全記憶體保護區內部進行純文字資料計算，藉以解決這些限制。 安全記憶體保護區是 SQL Server 處理序內受保護的記憶體區域，並可作為受信任的執行環境來處理 SQL Server 引擎內部的敏感性資料。 安全記憶體保護區對於主控電腦上其餘部分的 SQL Server 和其他處理序會顯示為黑盒子。 即使使用偵錯工具，也沒有辦法從外部檢視記憶體保護區內部的任何資料或程式碼。  


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
> 在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中，豐富計算會暫止數個效能最佳化 (包含無編製索引等這類有限功能)，而且目前預設會予以停用。 若要啟用豐富計算，請參閱[啟用豐富計算](configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中，具有安全記憶體保護區的 Always Encrypted 會使用[虛擬式安全性 (VBS)](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) \(英文\) 來保護 Windows 中的記憶體保護區 (也稱為虛擬安全模式或 VSM 記憶體保護區)。

## <a name="secure-enclave-attestation"></a>安全記憶體保護區證明

SQL Server 引擎內部的安全記憶體保護區能夠以純文字形式存取加密資料庫資料行中儲存的敏感性資料與對應的資料行加密金鑰。 將涉及記憶體保護區計算的查詢提交給 SQL Server 之前，應用程式內部的用戶端驅動程式必須確認安全記憶體保護區是根據指定技術 (例如 VBS) 的真正記憶體保護區，而且已簽署在記憶體保護區內部執行的程式碼，以便在記憶體保護區內部執行。 

確認記憶體保護區的處理序稱為**記憶體保護區證明**，它通常包含應用程式 (有時也包括 SQL Server) 內的用戶端驅動程式與外部證明服務連絡。 證明處理序的細節取決於記憶體保護區技術和證明服務。

SQL Server 在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中支援 VBS 安全記憶體保護區的證明處理序是 Windows Defender 系統防護執行階段證明，它會使用主機守護者服務 (HGS) 作為證明服務。 您需要在環境中設定 HGS，並在 HGS 中註冊裝載 SQL Server 執行個體的電腦。 您還必須使用 HGS 證明來設定用戶端應用程式或工具 (例如 SQL Server Management Studio)。

## <a name="secure-enclave-providers"></a>安全記憶體保護區提供者

若要使用具有安全記憶體保護區的 Always Encrypted，應用程式必須使用支援此功能的用戶端驅動程式。 在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中，您的應用程式必須使用 .NET Framework 4.7.2 和 .NET Framework Data Provider for SQL Server。 此外，.NET 應用程式還必須設有記憶體保護區類型 (例如 VBS) 專用的 **安全記憶體保護區提供者**，以及您要使用的證明服務 (例如 HGS)。 支援的記憶體保護區提供者隨附於個別 NuGet 套件，您必須將其與您的應用程式整合。 記憶體保護區提供者會實作用戶端邏輯，用於證明通訊協定以及與指定類型的記憶體保護區建立安全通道。

## <a name="enclave-enabled-keys"></a>已啟用記憶體保護區的金鑰

具有安全記憶體保護區的 Always Encrypted 引入了已啟用記憶體保護區的金鑰概念：

- **已啟用記憶體保護區的資料行主要金鑰** - 在資料庫內部資料行主要金鑰中繼資料物件中已指定 ENCLAVE_COMPUTATIONS 屬性的資料行主要金鑰。 資料行主要金鑰中繼資料物件也必須包含中繼資料屬性的有效簽章。
- **已啟用記憶體保護區的資料行加密金鑰** - 以已啟用記憶體保護區的資料行主要金鑰進行加密的資料行加密金鑰。

當 SQL Server 引擎判斷查詢中指定的作業需要在安全記憶體保護區內部執行時，SQL Server 引擎會要求用戶端驅動程式共用使用安全記憶體保護區進行計算所需的資料行加密金鑰。 只有在金鑰是已啟用記憶體保護區的金鑰 (亦即，以已啟用記憶體保護區的資料行主要金鑰進行加密)，並已正確簽署時，用戶端驅動程式才會共用資料行加密金鑰。 否則，此查詢會失敗。

## <a name="enclave-enabled-columns"></a>已啟用記憶體保護區的資料行

已啟用記憶體保護區的資料行是以已啟用記憶體保護區資料行加密金鑰進行加密的資料庫資料行。 已啟用記憶體保護區資料行可使用的功能取決於資料行所使用加密類型。

- **確定性加密** - 已啟用記憶體保護區的資料行若使用確定性加密，就能在安全記憶體保護區內部支援就地加密，但不支援任何其他作業。 透過比較加密文字 (記憶體保護區外部) 支援相等比較，但它是在記憶體保護區外部執行。  
- **隨機化加密** - 已啟用記憶體保護區的資料行若使用隨機化加密，就能在安全記憶體保護區內部支援就地加密及豐富計算。 支援的豐富計算是模式比對和[比較運算子](https://docs.microsoft.com/sql/t-sql/language-elements/comparison-operators-transact-sql)，包括相等比較。

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

## <a name="known-limitations"></a>已知限制

一般限制： 

- 列在 Always Encrypted 目前版本[功能詳細資料](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine#feature-details)中之所有限制也適用於具有安全記憶體保護區的 Always Encrypted (以已啟用記憶體保護區金鑰進行加密的資料行)，但由新增支援就地加密和豐富計算而移除的限制除外。

- 相等比較仍然是確定性加密支援的唯一 Transact-SQL 運算子，而且無論資料行加密金鑰是否為已啟用記憶體保護區的金鑰，相等比較都會在記憶體保護區外部透過比較加密文字值來執行。 以已啟用記憶體保護區的資料行加密金鑰進行確定性加密時，唯一解除鎖定的新功能是就地密碼編譯作業。 如果您有使用確定性加密 (和未已啟用記憶體保護區的金鑰) 加密的資料行，若要啟用豐富計算 (模式比對、比較作業)，您需要使用隨機化加密重新加密資料行。

- 使用定序的現有限制適用於以已啟用記憶體保護區資料行加密金鑰進行加密的資料行：使用確定性加密的字元字串資料行 (char、nchar、varchar、nvarchar) 必須使用具有 binary2 排序順序的定序 (BIN2 定序)。 使用非 BIN2 定序的字元字串資料行可以使用隨機化加密進行加密；不過，對這類資料行 (如果它們是以已啟用記憶體保護區的資料行加密金鑰進行加密) 啟用的唯一新功能是就地加密。 **為了支援豐富計算 (模式比對、比較作業)，資料行必須使用 BIN2 定序** (且資料行必須使用隨機化加密和已啟用記憶體保護區的資料行加密金鑰進行加密)。

- 不支援對記憶體內部資料表中的資料行使用已啟用記憶體保護區的金鑰。

- 除了定序和 Null 屬性的變更以外，就地密碼編譯作業無法與資料行中繼資料的任何其他變更合併。 例如，您無法加密、重新加密或解密資料行，同時變更單一 ALTER TABLE 或 ALTER COLUMN TRANSACT-SQL 陳述式中的資料行資料類型。 您需要使用兩個個別的陳述式。

下列限制適用於目前的預覽版本，但已納入要解決的藍圖中：

- 使用隨機化加密且已啟用記憶體保護區的資料行無法編製索引，這表示該比較作業或 LIKE 作業需要資料表掃描。

- 針對具有安全記憶體保護區的 Always Encrypted，唯一支援此功能的用戶端驅動程式是 .NET Framework 4.7.2 中的 .NET Framework Data Provider for SQL Server (ADO.NET)。 沒有 ODBC/JDBC 支援。

- 若要儲存已啟用記憶體保護區的資料行主要金鑰，唯一支援的金鑰存放區是 Windows 憑證存放區和 Azure Key Vault。

- 針對具有安全記憶體保護區的 Always Encrypted，目前的工具支援並不完整。 若要透過 ALTER TABLE Transact-SQL 陳述式觸發就地密碼編譯作業，您必須使用 SSMS 中的查詢視窗發出陳述式，也可以撰寫自己的程式來發出陳述式。 SqlServer PowerShell 模組中的 Set-SqlColumnEncryption Cmdlet 和 SQL Server Management Studio 中的 [Always Encrypted 精靈] 尚未支援就地加密，即使用於作業之資料行加密金鑰是已啟用記憶體保護區的金鑰，但這兩個工具目前會將資料移出資料庫以進行密碼編譯作業。 

## <a name="known-issues"></a>已知問題

- 非 UNICODE (char、varchar) 字串資料行的豐富計算需要在資料庫層級設定 BIN2 定序。 請參閱[管理定序](configure-always-encrypted-enclaves.md#manage-collations)中的＜非 UNICODE 字串資料行的特殊考量＞。

## <a name="next-steps"></a>Next Steps

- 設定測試環境並在 SSMS 中嘗試具有安全記憶體保護區的 Always Encrypted 功能，請參閱[教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)。