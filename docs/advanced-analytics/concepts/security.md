---
title: R 和 Python 擴充功能的安全性總覽
description: SQL Server Machine Learning 服務中擴充性架構的安全性總覽。 登入和使用者帳戶、SQL Server Launchpad 服務、背景工作帳戶、執行多個腳本和檔案許可權的安全性。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 39a9d05761b60878f1d7856378ba4cb28e54e2f9
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470474"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services 中擴充性架構的安全性總覽

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明用來整合 SQL Server 資料庫引擎和相關元件與擴充性架構的整體安全性架構。 它會檢查安全性實體、服務、處理常式身分識別和許可權。 如需 SQL Server 中擴充性的重要概念和元件的詳細資訊, 請參閱[SQL Server Machine Learning Services 中](extensibility-framework.md)的擴充性架構。

## <a name="securables-for-external-script"></a>外部腳本的安全性實體

以 R 或 Python 撰寫的外部腳本會以輸入參數的形式提交給針對此用途所建立的[系統預存](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)程式, 或包裝在您定義的預存程式中。 或者, 您可能會有在資料庫資料表中以二進位格式預先定型和儲存的模型, 並可在 T-sql [PREDICT](../../t-sql/queries/predict-transact-sql.md)函數中呼叫。

由於腳本是透過現有的資料庫架構物件、預存程式和資料表來提供, 因此 SQL Server Machine Learning 服務沒有新的[安全性實體](../../relational-databases/security/securables.md)。

無論您使用腳本的方式為何, 或其組成的內容為何, 將會建立資料庫物件並可能儲存, 但不會引進新的物件類型來儲存腳本。 因此, 取用、建立和儲存資料庫物件的能力, 主要取決於已經為您的使用者定義的資料庫許可權。

<a name="permissions"></a>

## <a name="permissions"></a>Permissions

SQL Server 的資料庫登入和角色的資料安全性模型會延伸至 R 和 Python 腳本。 需要 SQL Server 登入或 Windows 使用者帳戶, 才能執行使用 SQL Server 資料或以 SQL Server 執行的外部腳本作為計算內容。 擁有執行臨機操作查詢許可權的資料庫使用者, 可以從 R 或 Python 腳本存取相同的資料。

登入或使用者帳戶會根據外部腳本需求, 識別可能需要多個存取層級的*安全性主體*:

+ 存取已啟用外部腳本之資料庫的許可權。
+ 從受保護的物件 (例如資料表) 讀取資料的許可權。
+ 將新資料寫入資料表 (例如模型) 或評分結果的功能。
+ 建立新物件 (例如資料表、使用外部腳本的預存程式, 或使用 R 或 Python 作業的自訂函數) 的功能。
+ 在 SQL Server 電腦上安裝新封裝, 或使用提供給一組使用者的套件的許可權。

使用 SQL Server 做為執行內容之外部腳本的每個人, 都必須對應到資料庫中的使用者。 您可以建立角色來管理許可權集, 並將使用者指派給這些角色, 而不是個別設定使用者許可權, 而不是個別設定資料庫使用者權限。

如需詳細資訊, 請參閱[授與使用者 SQL Server Machine Learning 服務的許可權](../../advanced-analytics/security/user-permission.md)。

## <a name="permissions-when-using-an-external-client-tool"></a>使用外部用戶端工具時的許可權

如果使用者需要在資料庫中執行外部腳本, 或存取資料庫物件和資料, 則在外部用戶端工具中使用 R 或 Python 的使用者必須將其登入或帳戶對應至資料庫中的使用者。 無論是從遠端資料科學用戶端傳送外部腳本, 或使用 T-sql 預存程式執行, 都需要相同的許可權。

例如, 假設您建立了在本機電腦上執行的外部腳本, 而您想要在 SQL Server 上執行該腳本。 您必須確認符合下列條件：

+ 該資料庫允許遠端連線。
+ 您用來存取資料庫的 SQL 登入或 Windows 帳戶, 已加入實例層級的 SQL Server。
+ SQL 登入或 Windows 使用者必須擁有執行外部腳本的許可權。 一般而言，只有資料庫管理員可以授與此權限。
+ 您必須在每個資料庫中, 將 SQL 登入或視窗使用者新增為具有適當許可權的使用者, 其中外部腳本會執行下列任何作業:
  + 正在抓取資料。
  + 寫入或更新資料。
  + 建立新的物件, 例如資料表或預存程式。

在布建登入或 Windows 使用者帳戶並提供必要的許可權之後, 您可以使用 R 中的資料來源物件或 Python 中的**revoscalepy**程式庫或呼叫預存程式, 在 SQL Server 上執行外部腳本。包含外部腳本。

每當從 SQL Server 啟動外部腳本時, 資料庫引擎安全性就會取得啟動工作之使用者的安全性內容, 並管理使用者的對應或登入安全物件。

因此, 從遠端用戶端起始的所有外部腳本, 都必須將登入或使用者資訊指定為連接字串的一部分。

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>外部處理 (啟動列) 中使用的服務

擴充性架構會在 SQL Server 安裝的[服務清單](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details)中加入一個新的 NT 服務:[**SQL Server Launchpad (MSSSQLSERVER)** ](extensibility-framework.md#launchpad)。

資料庫引擎會使用 SQL Server Launchpad 服務, 將 R 或 Python 會話具現化為個別的進程。 進程會以低許可權帳戶執行;有別于 SQL Server、啟動列本身, 以及用來執行預存程式或主查詢的使用者識別。 在 [低許可權帳戶] 底下的個別進程中執行腳本, 是 SQL Server 中 R 和 Python 的安全性和隔離模型的基礎。

除了啟動外部進程之外, 啟動列也會負責追蹤呼叫使用者的身分識別, 並將該身分識別對應至用來啟動進程的低許可權背景工作角色帳戶。 在某些情況下, 腳本或程式碼會回呼以 SQL Server 資料和作業, 啟動列通常可以順暢地管理身分識別傳輸。 如果呼叫的使用者有足夠的許可權, 則包含 SELECT 語句或呼叫函式和其他程式設計物件的腳本通常會成功。

> [!NOTE]
> 根據預設, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]會設定為在**NT Service\MSSQLLaunchpad**下執行, 這會以所有必要的許可權布建, 以執行外部腳本。 如需可設定選項的詳細資訊, 請參閱[SQL Server Launchpad 服務](../security/sql-server-launchpad-service-account.md)設定。

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>用於處理的身分識別 (SQLRUserGroup)

**SQLRUserGroup**(SQL 受限的使用者群組) 是由 SQL Server 安裝程式所建立, 包含低許可權本機 Windows 使用者帳戶的集區。 需要外部進程時, 啟動列會取得可用的背景工作帳戶, 並使用它來執行處理常式。 更明確地說, 啟動列會啟用可用的背景工作帳戶、將其對應至呼叫使用者的身分識別, 並在背景工作帳戶底下執行腳本。

+ **SQLRUserGroup**會連結至特定的實例。 已啟用機器學習服務的每個實例都需要不同的背景工作帳戶集區。 執行個體之間的帳戶無法共用。

+ 使用者帳戶集區的大小是靜態的, 預設值是 20, 它支援20個並行會話。 可以同時啟動的外部執行時間會話數目, 受限於此使用者帳戶集區的大小。 

+ 集區中的背景工作帳戶名稱格式為 SQLInstanceName*nn*。 例如, 在預設的實例上, **SQLRUserGroup**包含名為 MSSQLSERVER01、MSSQLSERVER02, 依此類推的帳戶, 最多可達 MSSQLSERVER20。

平行處理的工作不會耗用其他帳戶。 例如, 如果使用者執行使用平行處理的評分工作, 則會對所有線程重複使用相同的工作者帳戶。 如果您想要大量使用機器學習服務, 您可以增加用來執行外部腳本的帳戶數目。 如需詳細資訊, 請參閱[修改機器學習服務的使用者帳戶集](../../advanced-analytics/administration/modify-user-account-pool.md)區。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>SQL Server 2019 中的 AppContainer 隔離

在 SQL Server 2019 中, 安裝程式不再建立**SQLRUserGroup**的背景工作帳戶。 相反地, 隔離是透過[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)來達成。 在執行時間, 在預存程式或查詢中偵測到外部腳本時, SQL Server 會使用延伸模組特定啟動器的要求來呼叫啟動控制板。 啟動列會在其身分識別的進程中叫用適當的執行時間環境, 並具現化 AppContainer 以包含它。 這種變更很有用, 因為已不再需要本機帳戶和密碼管理。 此外, 在禁止本機使用者帳戶的安裝上, 刪除本機使用者帳戶相依性表示您現在可以使用這項功能。

AppContainers 由 SQL Server 實作為內部機制。 雖然您不會在進程監視器中看到 AppContainers 的實體辨識項, 但是您可以在安裝程式所建立的輸出防火牆規則中找到它們, 以避免進程進行網路呼叫。 如需詳細資訊, 請參閱[SQL Server Machine Learning 服務的防火牆](../../advanced-analytics/security/firewall-configuration.md)設定。

> [!Note]
> 在 SQL Server 2019 中, **SQLRUserGroup**只有一個成員, 現在是單一 SQL Server Launchpad 服務帳戶, 而不是多個背景工作帳戶。
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>授與 SQLRUserGroup 的許可權

根據預設, **SQLRUserGroup**的成員具有 SQL Server **Binn**、 **R_SERVICES**和**PYTHON_SERVICES**目錄中檔案的讀取和執行許可權, 以及 R 中的可執行檔、程式庫和內建資料集的存取權。和與 SQL Server 一起安裝的 Python 散發套件。 

若要保護 SQL Server 上的機密資源, 您可以選擇性地定義存取控制清單 (ACL), 以拒絕**SQLRUserGroup**的存取權。 相反地, 您也可以將許可權授與存在於主機電腦上的本機資料資源, 與 SQL Server 本身分開。 

根據設計, **SQLRUserGroup**沒有任何資料的資料庫登入或許可權。 在某些情況下, 您可能會想要建立登入以允許迴圈後的連線, 特別是當受信任的 Windows 身分識別為呼叫使用者時。 這項功能稱為「[*隱含的驗證*](#implied-authentication)」。 如需詳細資訊, 請參閱[將 SQLRUserGroup 新增為資料庫使用者](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)。

## <a name="identity-mapping"></a>識別對應

當會話啟動時, 啟動列會將呼叫使用者的身分識別對應至背景工作帳戶。 外部 Windows 使用者或有效 SQL 登入到背景工作帳戶的對應, 只有在執行外部腳本的 SQL 預存程式存留期間才有效。 來自相同登入的平行查詢會對應到相同的使用者背景工作帳戶。

在執行期間, 啟動列會建立暫存資料夾來儲存會話資料, 並在會話結束時將它們刪除。 目錄受到存取限制。 針對 R, RLauncher 會執行這項工作。 針對 Python, PythonLauncher 會執行這項工作。 每個個別的背景工作帳戶僅限於自己的資料夾, 而且無法存取其本身層級上方資料夾中的檔案。 不過, 工作者帳戶可以讀取、寫入或刪除所建立之會話工作資料夾下的子系。 如果您是該電腦上的系統管理員，您可以檢視針對每個處理序所建立的目錄。 每個目錄是以其工作階段 GUID 來識別。

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>隱含驗證 (迴圈送回要求)

「*隱含的驗證*」描述連接要求的行為, 在此情況下, 以低許可權背景工作角色帳戶執行的外部進程會呈現為受信任的使用者身分識別, 以 SQL Server 對資料或作業的迴圈送回要求 就概念而言, 隱含驗證對於 Windows 驗證而言是唯一的, 在 SQL Server 連接字串中指定信任的連線, 在來自 R 或 Python 腳本等外部進程的要求上。 有時候也稱為「*迴圈*」。

信任的連線可從 R 和 Python 腳本運作, 但只適用于額外的設定。 在擴充性架構中, R 和 Python 進程會在背景工作帳戶下執行, 並繼承父**SQLRUserGroup**的許可權。 當連接字串指定`Trusted_Connection=True`時, 背景工作帳戶的身分識別會顯示在連線要求上, 預設為 [未知] 以 SQL Server。

若要讓信任連接成功, 您必須建立**SQLRUserGroup**的資料庫登入。 在這麼做之後, 任何來自**SQLRUserGroup**成員的信任連接都有登入許可權可 SQL Server。 如需逐步指示, 請參閱[將 SQLRUserGroup 新增至資料庫登](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)入。

信任的連線不是最廣泛使用的連線要求形式。 當 R 或 Python 腳本指定連接時, 如果連接到 ODBC 資料來源, 則使用 SQL 登入或完整指定的使用者名稱和密碼可能會更常見。

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>R 和 Python 會話的隱含驗證運作方式

下圖顯示 SQL Server 元件與 R 執行時間的互動, 以及它如何執行 R 的隱含驗證。

![R 的隱含驗證](../security/media/implied-auth-rsql.png)

下圖顯示 SQL Server 元件與 Python 執行時間的互動, 以及它如何執行 Python 的隱含驗證。

![Python 的隱含驗證](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>不支援待用透明資料加密

[透明資料加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)不支援從外部腳本執行時間傳送或接收的資料。 原因是外部進程 (R 或 Python) 是在 SQL Server 進程之外執行。 因此, 外部執行時間所使用的資料並不受 database engine 的加密功能所保護。 這種行為與在 SQL Server 電腦上執行的任何其他用戶端不同, 它會從資料庫讀取資料並建立複本。

因此, TDE 不會套用至您在 R 或 Python 腳本中使用的任何資料, 也**不會**套用至任何儲存至磁片的資料, 或任何保存的中繼結果。 不過, 其他類型的加密 (例如, 在檔案或資料夾層級套用的 Windows BitLocker 加密或協力廠商加密) 仍適用。

在[Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)的情況下, 外部執行時間不會有加密金鑰的存取權。 因此, 無法將資料傳送至腳本。

## <a name="next-steps"></a>後續步驟

在本文中, 您已瞭解內建于擴充性[架構](../../advanced-analytics/concepts/extensibility-framework.md)之安全性架構的元件和互動模型。 本文涵蓋的重點包括: 啟動控制板、SQLRUserGroup 和背景工作帳戶、R 和 Python 的進程隔離, 以及使用者身分識別如何對應至背景工作帳戶。 

在下一個步驟中, 請參閱授與[許可權](../../advanced-analytics/security/user-permission.md)的指示。 針對使用 Windows 驗證的伺服器, 您也應該參閱[將 SQLRUserGroup 新增至資料庫登](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)入, 以瞭解何時需要額外的設定。