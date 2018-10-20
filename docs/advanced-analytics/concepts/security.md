---
title: 適用於 SQL Server machine learning 的安全性 |Microsoft Docs
description: SQL Server Machine Learning 服務的擴充性架構的安全性概觀。 登入和使用者帳戶、 SQL Server Launchpad 服務、 背景工作帳戶，執行多個指令碼和檔案權限的安全性。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: a5d109e16c81481f9e4267dc4963ecea74cfa736
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419373"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning 服務的擴充性架構的安全性概觀

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明用來整合擴充性架構中的 SQL Server 資料庫引擎和相關的元件的整體安全性架構。 它會檢查安全性實體、 服務、 處理序識別和權限。 如需有關的重要概念和 SQL Server 中的擴充性元件的詳細資訊，請參閱[SQL Server Machine Learning 服務中的擴充性架構](extensibility-framework.md)]。

## <a name="securables-for-external-script"></a>外部指令碼的安全性實體

以 R 或 Python 撰寫的外部指令碼做為輸入參數來送出[系統預存程序](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)建立基於此目的，或是會包裝在您定義的預存程序。 或者，您可能會預先定型並儲存在資料庫資料表時，可呼叫在 T-SQL 中的二進位格式的模型[PREDICT](../../t-sql/queries/predict-transact-sql.md)函式。

指令碼透過現有的資料庫結構描述物件、 預存程序和資料表提供，如有任何新[安全性實體](../../relational-databases/security/securables.md)for SQL Server Machine Learning 服務。

不論您使用指令碼的方式，或它們組成，會建立資料庫物件，並可能儲存，但沒有新的物件類型來儲存指令碼導入。 如此一來，可使用，建立和儲存資料庫物件主要取決於已為您的使用者定義的資料庫權限。

<a name="permissions"></a>

## <a name="permissions"></a>Permissions

SQL Server 的資料安全性模型的資料庫登入和角色將延伸到 R 和 Python 指令碼。 SQL Server 登入或 Windows 使用者帳戶，才能執行外部指令碼，使用 SQL Server 資料，或包含執行與 SQL Server 計算內容。 若要執行臨機操作查詢的權限的資料庫使用者可以存取相同的資料，從 R 或 Python 指令碼。

登入或使用者帳戶識別*安全性主體*，可能需要多個層級的存取，根據外部指令碼需求的使用者：

+ 存取的資料庫，啟用外部指令碼的權限。
+ 若要從受保護的物件，例如資料表讀取資料的權限。
+ 能夠將新的資料寫入至資料表，例如模型或評分結果。
+ 能夠建立新的物件，例如資料表、 預存程序，使用外部指令碼，或自訂函式，該使用 R 或 Python 作業。
+ SQL Server 電腦上安裝新套件或使用套件提供給一群使用者權限。

執行外部指令碼使用 SQL Server 的執行內容為每個人員必須對應至資料庫中的使用者。 而不是個別設定資料庫使用者權限，您可以建立角色，以管理集合的權限，並將使用者指派給這些角色，而不是個別設定 使用者權限。

如需詳細資訊，請參閱 < [SQL Server Machine Learning 服務的權限授與使用者](../../advanced-analytics/security/user-permission.md)。

## <a name="permissions-when-using-an-external-client-tool"></a>使用外部的用戶端工具時的權限

使用 R 或 Python 中的外部用戶端工具的使用者必須具有其登入或帳戶對應至資料庫中的使用者，如果他們需要執行外部指令碼在資料庫或 access 資料庫物件和資料。 相同的權限所需從遠端資料科學用戶端是否傳送外部指令碼，或使用 T-SQL 預存程序執行。

例如，假設您建立您的本機電腦上執行外部指令碼，以及您想要在 SQL Server 上執行該指令碼。 您必須確認符合下列條件：

+ 該資料庫允許遠端連線。
+ SQL 登入或您用來進行資料庫存取權的 Windows 帳戶已新增至 SQL Server 執行個體層級。
+ SQL 登入或 Windows 使用者必須執行外部指令碼的權限。 一般而言，只有資料庫管理員可以授與此權限。
+ SQL 登入或 Window 使用者必須新增為使用者，具有適當的權限，其中外部指令碼會執行任何這些作業的每個資料庫中：
  + 正在擷取資料。
  + 寫入或更新資料。
  + 建立新的物件，例如資料表或預存程序。

登入或 Windows 使用者帳戶已佈建並具有必要的權限之後，您可以藉由在 R 中使用資料來源物件在 SQL Server 上執行外部指令碼或**revoscalepy**在 Python 中，或藉由呼叫預存的程式庫包含外部指令碼的程序。

從 SQL Server 啟動外部指令碼時，每當資料庫引擎安全性取得啟動工作，及管理對應的使用者或登入安全性實體物件之使用者的安全性內容。

因此，從遠端用戶端起始的所有外部指令碼必須登入或使用者資訊指定為連接字串的一部分。

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>外部處理 （啟動控制板） 中所用的服務

擴充性架構新增一個新 NT 服務才[的服務清單](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details)SQL Server 安裝中： [ **SQL Server Launchpad (MSSSQLSERVER)**](extensibility-framework.md#launchpad)。

Database engine 會使用 SQL Server Launchpad 服務，具現化的 R 或 Python 的工作階段做為個別的處理序。 此程序的帳戶下執行低權限;不同於 SQL Server、 啟動控制板本身，以及執行預存程序或主應用程式查詢使用者識別。 以個別的處理序，在低權限帳戶下執行指令碼是 R 和 Python 中 SQL Server 的安全性和隔離模型的基礎。

除了啟動外部處理序，啟動控制板也會負責追蹤呼叫使用者的身分識別，並將該身分識別對應至用來啟動處理序的低權限背景工作帳戶。 在某些情況下，其中指令碼或程式碼回呼至 SQL Server 資料和作業，Launchpad 會通常能夠順暢地管理身分識別的傳輸。 如果呼叫的使用者有足夠的權限，包含 SELECT 陳述式或呼叫函式和其他程式設計物件的指令碼通常會成功。

> [!NOTE]
> 根據預設，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]設定為執行之下**NT Service\MSSQLLaunchpad**，這將會佈建所有必要的權限執行外部指令碼。 如需可設定選項的詳細資訊，請參閱[SQL Server Launchpad 服務組態](../security/sql-server-launchpad-service-account.md)。

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>在用來處理 (SQLRUserGroup) 的身分識別

**SQLRUserGroup** （SQL 受限的使用者群組） 會建立 SQL Server 安裝程式，並包含的低權限本機 Windows 使用者帳戶集區。 當需要外部處理序時，Launchpad 會使用背景工作帳戶，並使用它來執行程序。 更具體來說，Launchpad 啟動可用的工作者帳戶、 將它對應至呼叫的使用者的身分識別和執行指令碼的背景工作帳戶。

+ **SQLRUserGroup**連結到特定的執行個體。 Machine learning 已啟用每個執行個體需要不同的集區的背景工作帳戶。 執行個體之間的帳戶無法共用。

+ 使用者帳戶集區的大小是靜態和預設值為 20，可支援 20 個並行工作階段。 可同時啟動的外部執行階段工作階段數目受限於此使用者帳戶集區的大小。 

+ 背景工作角色集區中的帳戶名稱為格式為 SQLInstanceName*nn*。 例如，在預設執行個體上**SQLRUserGroup**包含帳戶上名為 MSSQLSERVER01、 MSSQLSERVER02，依此類推到 MSSQLSERVER20。

平行的工作並不會耗用額外的帳戶。 比方說，如果使用者執行的計分工作使用平行處理，將相同的背景工作帳戶會重複使用的所有執行緒中。 如果您想要大量使用機器學習服務，您可以增加帳戶用來執行外部指令碼數目。 如需詳細資訊，請參閱 <<c0> [ 修改使用者帳戶集區，適用於 machine learning](../../advanced-analytics/administration/modify-user-account-pool.md)。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>在 SQL Server 2019 AppContainer 隔離

在 SQL Server 2019，安裝程式不會再建立背景工作帳戶**SQLRUserGroup**。 相反地，透過來達成隔離[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)。 在執行階段，在預存程序或查詢中偵測到外部指令碼時，SQL Server 會呼叫啟動控制板，並要求延伸模組特定程式啟動器。 啟動控制板叫用其身分的處理序中的適當的執行階段環境，並包含該 AppContainer 具現化。 這項變更是有幫助，因為不再需要本機帳戶和密碼管理。 此外，其中禁止使用本機使用者帳戶的安裝，刪除本機使用者帳戶相依性表示您現在可以使用這項功能。

實作 SQL server 時，AppContainers 會是內部的機制。 雖然您不會看到 AppContainers Process Monitor 中的實體的辨識項，您可以找到它們，以防止處理程序進行網路呼叫的安裝程式所建立的輸出防火牆規則中。 如需詳細資訊，請參閱 < [SQL Server Machine Learning 服務的防火牆設定](../../advanced-analytics/security/firewall-configuration.md)。

> [!Note]
> 在 SQL Server 2019， **SQLRUserGroup**只有一個成員現在是單一的 SQL Server Launchpad 服務帳戶，而不是多個背景工作帳戶。
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>SQLRUserGroup 授與權限

根據預設，成員**SQLRUserGroup**具有讀取和執行 SQL Server 中的檔案權限**Binn**， **R_SERVICES**，和**PYTHON_SERVICES**目錄的存取權可執行檔、 程式庫，以及與 SQL Server 一起安裝的 R 和 Python 散發套件中的內建資料集。 

若要保護 SQL Server 上的敏感資源，您可以選擇性地定義會拒絕存取的存取控制清單 (ACL) **SQLRUserGroup**。 相反地，您也可以存在於主機電腦，除了 SQL Server 本身的本機資料資源的權限授與。 

根據設計， **SQLRUserGroup**不具有資料庫登入或任何資料的權限。 在某些情況下，您可能想要建立以便迴圈後的連線，尤其是受信任的 Windows 身分識別會呼叫使用者的登入。 這項功能稱為[*隱含的驗證*](#implied-authentication)。 如需詳細資訊，請參閱 <<c0> [ 為資料庫使用者的新增 SQLRUserGroup](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)。

## <a name="identity-mapping"></a>識別對應

當工作階段啟動時，Launchpad 會對應至背景工作帳戶的呼叫使用者的身分識別。 外部 Windows 使用者或背景工作帳戶的有效 SQL 登入的對應無效，只針對存留期的 sql 預存程序時，才執行外部指令碼。 來自相同登入的平行查詢會對應到相同的使用者背景工作帳戶。

在執行期間，Launchpad 會建立暫存資料夾來儲存工作階段資料，工作階段結束時刪除它們。 目錄是限制存取。 針對 R，RLauncher 會執行這項工作。 對於 Python，PythonLauncher 會執行這項工作。 每個個別的背景工作帳戶限制為自己的資料夾，且無法存取自己的層級上面的資料夾中的檔案。 不過，將背景工作帳戶可以讀取、 寫入或刪除已建立的工作階段工作資料夾下的子系。 如果您是該電腦上的系統管理員，您可以檢視針對每個處理序所建立的目錄。 每個目錄是以其工作階段 GUID 來識別。

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>隱含的驗證 （迴圈後要求）

*隱含的驗證*描述在其下執行時，低權限背景工作帳戶會做為受信任的使用者身分識別到 SQL Server 上的外部處理序迴圈後的要求資料或作業的連接要求行為。 概念上，隱含的驗證是源自於外部的程序，例如 R 或 Python 指令碼的要求上指定信任的連接，SQL Server 連接字串中的 Windows 驗證，唯一的。 它有時也稱為*迴圈*。

受信任的連線是可從 R 和 Python 指令碼，但僅限於有額外的設定。 在擴充性架構中，R 和 Python 程序則是背景工作帳戶，從父代繼承的權限下執行**SQLRUserGroup**。 當連接字串指定`Trusted_Connection=True`，連接要求時，也就是未知的 SQL Server 預設會顯示背景工作帳戶的身分識別。

若要讓受信任的連線成功，您必須建立的資料庫登入**SQLRUserGroup**。 完成後，任何受信任連線的任何成員**SQLRUserGroup**具有 SQL Server 登入權限。 如需逐步指示，請參閱 <<c0> [ 資料庫登入的新增 SQLRUserGroup](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)。

信任的連接不是最廣泛使用的形式的連線要求。 當 R 或 Python 指令碼指定的連接時，它可以是較常使用 SQL 登入，或是完整指定的使用者名稱和密碼，如果連接至 ODBC 資料來源。

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>R 和 Python 的工作階段如何隱含的驗證的運作方式

下圖顯示 SQL Server 元件的互動與 R 執行階段，以及它將會如何執行隱含的驗證，如。

![適用於 R 的隱含的驗證](../security/media/implied-auth-rsql.png)

下圖顯示的 Python 執行階段和它的運作適用於 Python 的隱含的驗證方式與 SQL Server 元件的互動。

![適用於 Python 的隱含的驗證](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>不支援透明資料加密待用

[透明資料加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)不支援從外部指令碼執行階段來傳送或接收的資料。 原因是外部處理序 （R 或 Python） 執行 SQL Server 處理序之外。 因此，database engine 的加密功能不受外部的執行階段所使用的資料。 此行為是沒什麼兩樣，從資料庫讀取資料，並建立其複本的 SQL Server 電腦上執行的其他任何用戶端。

因此，TDE**不是**套用至您使用 R 或 Python 指令碼中的任何資料或儲存至磁碟，或任何持續性的中繼結果的任何資料。 不過，其他類型的加密，例如 Windows BitLocker 加密或協力廠商加密套用到檔案或資料夾層級，仍然適用。

若是[Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)，外部執行階段並沒有加密金鑰的存取權。 因此，資料無法傳送至指令碼。

## <a name="next-steps"></a>後續步驟

在本文中，您學到的元件，並內建的安全性架構的互動模型[擴充性架構](../../advanced-analytics/concepts/extensibility-framework.md)。 本文章涵蓋的重點包括用途的啟動列 」、 「 SQLRUserGroup 和 「 背景工作帳戶的 R 和 Python，以及如何將使用者身分識別對應至背景工作帳戶的處理序隔離。 

下一個步驟中，檢閱的指示[授與權限](../../advanced-analytics/security/user-permission.md)。 使用 Windows 驗證的伺服器，您也應該檢閱[資料庫登入的新增 SQLRUserGroup](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)若要了解何時需要額外的設定。