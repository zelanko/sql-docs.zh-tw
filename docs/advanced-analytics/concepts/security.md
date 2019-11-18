---
title: 擴充性的安全性概觀
description: SQL Server 機器學習服務中擴充性架構的安全性概觀。 登入與使用者帳戶、SQL Server Launchpad 服務、背景工作角色帳戶、執行多個指令碼及檔案權限的安全性。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f2e2d696a09e5b5bb321da583efd76f580759ce6
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727671"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server 機器學習服務中擴充性架構的安全性概觀

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文描述用來將 SQL Server 資料庫引擎和相關元件與擴充性架構整合的整體安全性架構。 它會檢查安全性實體、服務、處理序身分識別及權限。 如需有關 SQL Server 中擴充性之重要概念與元件的詳細資訊，請參閱 [SQL Server 機器學習服務的擴充性架構](extensibility-framework.md)]。

## <a name="securables-for-external-script"></a>外部指令碼的安全性實體

以 R 或 Python 撰寫的外部指令碼會提交為針對此目的建立之[系統預存程序](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的輸入參數，或會被包裝在您定義的預存程序中。 此外，您可能有在資料庫資料表中以二進位格式預先定型及儲存的模型，可在 T-SQL [PREDICT](../../t-sql/queries/predict-transact-sql.md) 函式中呼叫。

當指令碼透過現有的資料庫結構描述物件、預存程式與資料表提供時，SQL Server 機器學習服務沒有新的[安全性實體](../../relational-databases/security/securables.md)。

無論您使用指令碼的方式為何，或其組成內容為何，都會建立資料庫物件並可能儲存，但不會引進新的物件類型來儲存腳本。 因此，取用、建立及儲存資料庫物件的能力，主要取決於已經為您的使用者定義的資料庫權限。

<a name="permissions"></a>

## <a name="permissions"></a>權限

SQL Server 的資料庫登入與角色的資料安全性模型會延伸至 R 與 Python 指令碼。 需要 SQL Server 登入或 Windows 使用者帳戶，才能執行使用 SQL Server 資料或透過 SQL Server 以計算內容形式執行的外部指令碼。 擁有執行臨機操作查詢權限的資料庫使用者，可以從 R 或 Python 指令碼存取相同的資料。

登入或使用者帳戶會根據外部指令碼需求，識別可能需要多個存取層級的「安全性主體」  ：

+ 存取已啟用外部指令碼之資料庫的權限。
+ 從受保護的物件 (例如資料表) 讀取資料的權限。
+ 將新資料寫入資料表 (例如模型) 或評分結果的功能。
+ 建立新物件 (例如資料表、使用外部指令碼的預存程式，或使用 R 或 Python 作業的自訂函式) 的功能。
+ 在 SQL Server 電腦上安裝新套件，或使用提供給一組使用者之套件的權限。

使用 SQL Server 作為執行內容來執行外部指令碼的每個人，都必須對應到資料庫中的使用者。 您不需要個別設定資料庫使用者權限，而是可以建立角色來管理權限集合，並將使用者指派給那些角色，而不是個別設定使用者權限。

如需詳細資訊，請參閱[授與使用者 SQL Server 機器學習服務的權限](../../advanced-analytics/security/user-permission.md)。

## <a name="permissions-when-using-an-external-client-tool"></a>使用外部用戶端工具時的權限

在外部用戶端工具中使用 R 或 Python 的使用者必須將其登入或帳戶對應到資料庫中的使用者 (假設使用者需要在資料庫中執行外部指令碼，或存取資料庫物件與資料)。 不論外部指令碼傳送自遠端資料科學用戶端，或使用 T-SQL 預存程序執行，都需要相同的權限。

例如，假設您建立了在本機電腦上執行的外部指令碼，而且您想要在 SQL Server 上執行該指令碼。 您必須確認符合下列條件：

+ 該資料庫允許遠端連線。
+ 您為資料庫存取使用的 SQL 登入或 Windows 帳戶已加入到執行個體層級的 SQL Server。
+ SQL 登入或 Windows 使用者必須有執行外部指令碼的權限。 一般而言，只有資料庫管理員可以授與此權限。
+ 必須在以外部指令碼執行下列任一作業的每個資料庫中，將 SQL 登入或 Window 使用者新增為具有適當權限的使用者：
  + 擷取資料。
  + 寫入或更新資料。
  + 建立新物件，例如資料表或預存程序。

在佈建登入或 Windows 使用者帳戶並為其提供必要權限之後，您可以使用 R 中的資料來源物件或 Python 中的 **revoscalepy** 程式庫，或透過呼叫包含外部指令碼的預存程序，在 SQL Server 上執行外部指令碼。

每當從 SQL Server 啟動外部指令碼時，資料庫引擎都會取得啟動 R 工作之使用者的安全性內容，並且管理使用者或登入對安全性實體物件的對應。

因此，所有從遠端用戶端起始的外部指令碼，都必須將登入或使用者資訊指定為連接字串的一部分。

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>外部處理 (Launchpad) 中使用的服務

擴充性架構會將一個新的 NT 服務新增至 SQL Server 安裝中的[服務清單](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details)：[**SQL Server Launchpad (MSSSQLSERVER)** ](extensibility-framework.md#launchpad)。

資料庫引擎會使用 SQL Server Launchpad 服務，將 R 或 Python 工作階段具現化為個別處理序。 處理序會以低權限帳戶執行；這與 SQL Server、Launchpad 本身以及用來執行預存程序或主查詢的使用者識別有別。 以低權限帳戶在個別處理序中執行指令碼是 SQL Server 中 R 與 Python 的安全性與隔離模型的基礎。

除了啟動外部處理序之外，Launchpad 也會負責追蹤發出呼叫之使用者的身分識別，並將該身分識別對應到用來啟動處理序的低權限背景工作角色帳戶。 在指令碼或程式碼會針對資料與作業回呼 SQL Server 的某些情況下，Launchpad 通常可以順暢地管理身分識別移轉。 如果呼叫的使用者有足夠的權限，則包含 SELECT 陳述式或呼叫函式的指令碼與其他程式設計物件通常會成功。

> [!NOTE]
> 根據預設，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 會設定為在 **NT Service\MSSQLLaunchpad** 下執行，此帳戶已佈建用來執行外部指令碼的所有必要權限。 如需可設定選項的詳細資訊，請參閱 [SQL Server Launchpad 服務設定](../security/sql-server-launchpad-service-account.md)。

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>用於處理的身分識別 (SQLRUserGroup)

**SQLRUserGroup** (SQL 受限使用者群組) 是由 SQL Server 安裝程式所建立，而且包含低權限本機 Windows 使用者帳戶的集區。 需要外部處理序時，Launchpad 會取得可用的背景工作角色帳戶，並使用它來執行處理序。 更明確地說，Launchpad 會啟用可用的背景工作角色帳戶、將其對應到發出呼叫之使用者的身分識別，並在背景工作帳戶下執行指令碼。

+ **SQLRUserGroup** 連結到特定執行個體。 已啟用機器執行的每個執行個體上都需要背景工作角色角色帳戶的個別集區。 執行個體之間的帳戶無法共用。

+ 使用者帳戶集區的大小為靜態，預設值是 20，這支援 20 個同時工作階段。 可同時啟動的外部執行階段工作階段數目受限於此使用者帳戶集區大小。 

+ 集區中的背景工作角色帳戶名稱格式為 SQLInstanceName*nn*。 例如，在預設的執行個體上，**SQLRUserGroup** 包含名為 MSSQLSERVER01、MSSQLSERVER02、依此類推的帳戶 (最多 MSSQLSERVER20)。

平行處理的工作不會耗用其他帳戶。 例如，如果使用者執行使用平行處理的評分工作，則會為所有執行緒重複使用相同的背景工作角色帳戶。 如果您想要大量使用機器學習服務，您可以增加用來執行外部指令碼的帳戶數目。 如需詳細資訊，請參閱[修改機器學習的使用者帳戶集區](../../advanced-analytics/administration/modify-user-account-pool.md)。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>SQL Server 2019 中的 AppContainer 隔離

在 SQL Server 2019 中，安裝程式不會再為 **SQLRUserGroup** 建立背景工作角色帳戶。 而是透過 [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation) 來達成隔離。 在執行時，當在預存程序或查詢中偵測到外部指令碼時，SQL Server 會呼叫 Launchpad，並要求特定延伸模組的啟動器。 Launchpad 會在其身分識別的處理序中叫用適當的執行階段環境，並具現化 AppContainer 以包含它。 這種變更很有用，因為已不再需要本機帳戶和密碼管理。 此外，在禁止本機使用者帳戶的安裝上，去除本機使用者帳戶相依性表示您現在可以使用此功能。

正如 SQL Server 所實作，AppContainers 是一種內部機制。 雖然您不會在處理序監視器中看到 AppContainers 的實體辨識項，但是您可以在安裝程式所建立的輸出防火牆規則中找到它們，以避免處理序進行網路呼叫。 如需詳細資訊，請參閱 [SQL Server 機器學習服務的防火牆組態](../../advanced-analytics/security/firewall-configuration.md)。

> [!Note]
> 在 SQL Server 2019 中，**SQLRUserGroup** 只有一個成員，且現在是單一 SQL Server Launchpad 服務帳戶，而不是多個背景工作角色帳戶。
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>授與 SQLRUserGroup 的權限

根據預設，**SQLRUserGroup** 的成員具有 SQL Server **Binn**、**R_SERVICES** 與 **PYTHON_SERVICES** 目錄中檔案的讀取及執行權限，具有隨 SQL Server 安裝之 R 與 Python 發行版本的可執行檔、程式庫與內建資料集的存取權。 

若要保護 SQL Server 上的敏感性資源，您可以選擇性地定義存取控制清單 (ACL)，以拒絕對 **SQLRUserGroup** 的存取權。 相反地，您也可以授與主機電腦上本機資料來源的存取權，與 SQL Server 本身分開。 

根據設計，**SQLRUserGroup** 沒有任何資料的資料庫登入或權限。 在特定情況下，您可以建立登入以允許回送線，特別是當受信任的 Windows 身分識別為發出呼叫的使用者時。 此功能稱為[隱含驗證](#implied-authentication)  。 如需詳細資訊，請參閱[將 SQLRUserGroup 新增為資料庫使用者](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)。

## <a name="identity-mapping"></a>身分識別對應

當工作階段啟動時，Launchpad 會將發出呼叫之使用者的身分識別對應到背景工作角色帳戶。 外部 Windows 使用者或有效 SQL 登入對背景工作角色帳戶的對應，只在執行外部指令碼之 SQL 預存程序的生命週期內有效。 來自相同登入的平行查詢會對應到相同的使用者背景工作帳戶。

在執行期間，Launchpad 會建立暫存資料夾來儲存工作階段資料，並在工作階段結束時將其刪除。 目錄具有存取限制。 針對 R，RLauncher 會執行此工作。 針對 Python，PythonLauncher 會執行此 工作。 每個個別的背景工作角色帳戶僅限於自己的資料夾，而且無法存取其本身層級上方資料夾中的檔案。 不過，背景工作角色帳戶可以讀取、寫入或刪除所建立之工作階段工作資料夾下的子系。 如果您是該電腦上的系統管理員，您可以檢視針對每個處理序所建立的目錄。 每個目錄是以其工作階段 GUID 來識別。

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>隱含驗證 (回送要求)

*隱含驗證*描述連線要求行為，其中以低權限背景工作角色帳戶執行的外部處理序在資料或作業的回送要求上會顯示為 SQL Server 的受信任使用者身分識別。 就概念而言，隱含驗證對於 Windows 驗證而言是唯一的 (在指定受信任連線的SQL Server 連接字串中，或在來自外部處理序 (例如 R 或 Python 指令碼) 的要求上)。 這有時候也稱為「回送」  。

受信任的連線可從 R 與 Python 指令碼運作，但只適用於額外的設定。 在擴充性架構中，R 與 Python 處理序會在背景工作角色帳戶之下執行，繼承父系 **SQLRUserGroup** 的權限。 當連接字串指定 `Trusted_Connection=True` 時，背景工作角色帳戶的身分識別會顯示在連線要求上，SQL Server 預設不會知道此資訊。

若要讓受信任的連線成功，您必須為 **SQLRUserGroup** 建立資料庫登入。 這樣做之後，任何來自 **SQLRUserGroup** 成員的受信任連線都會有 SQL Server 的登入權限。 如需逐步指示，請參閱 [將 SQLRUserGroup 新增至資料庫登入](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)。

受信任的連線不是最廣泛使用的連線要求形式。 當 R 或 Python 指令碼指定連線時，如果是連線到 ODBC 資料來源，則使用 SQL 登入或完整指定的使用者名稱與密碼可能更常見。

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>R 與 Python 工作階段的隱含驗證如何運作

下圖顯示 SQL Server 元件與 R 執行階段的互動，以及它如何執行 R 的隱含驗證。

![R 的隱含驗證](../security/media/implied-auth-rsql.png)

下圖顯示 SQL Server 元件與 Python 執行階段的互動，以及它如何執行 Python 的隱含驗證。

![Python 的隱含驗證](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>不支援待用透明資料加密

從外部指令碼執行階段傳送或接收資料時，不支援[透明資料加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)。 原因是外部處理序 (R 或 Python) 是在 SQL Server 處理序之外執行。 因此，外部執行階段所使用的資料並不受資料庫引擎的加密功能所保護。 此行為與在 SQL Server 電腦上執行的任何其他用戶端不同，這些用戶端會從資料庫讀取資料並建立複本。

因此，TDE **不會**套用至您在 R 或 Python 指令碼中使用的任何資料、儲存到磁碟的任何資料或任何持續性中繼結果。 不過，其他類型的加密 (例如，在檔案或資料夾層級套用的 Windows BitLocker 加密或協力廠商加密) 仍適用。

在 [Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) 的情況下，外部執行階段不會有加密金鑰的存取權。 因此，資料無法傳送到指令碼。

## <a name="next-steps"></a>後續步驟

在此文章中，您已了解[擴充性架構](../../advanced-analytics/concepts/extensibility-framework.md)中內建之安全性架構的元件與互動模型。 此文章涵蓋的重點包括：Launchpad、SQLRUserGroup 與背景工作角色帳戶、R 與 Python 的處理序隔離的目的，以及使用者身分識別如何對應到背景工作角色帳戶。 

在下一個步驟中，請檢閱[授與權限](../../advanced-analytics/security/user-permission.md)的指示。 針對使用 Windows 驗證的伺服器，您也應該檢閱[將 SQLRUserGroup 新增至資料庫登入](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)，以了解何時需要額外的設定。