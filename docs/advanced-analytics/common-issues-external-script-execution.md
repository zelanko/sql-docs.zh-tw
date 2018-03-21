---
title: "SQL Server 中的外部指令碼執行的一般問題 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/11/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: af9896e9e0baa2899b9e9c95795907ca46463504
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2018
---
# <a name="common-issues-with-external-script-execution-in-sql-server"></a>SQL Server 中的外部指令碼執行的一般問題
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文包含已知的問題與 SQL Server 中執行 R 或 Python 程式碼的常見問題的清單。

開始之前，我們建議您先收集有關您的系統一些資訊。 若要了解作法，請參閱[的疑難排解資料收集](data-collection-ml-troubleshooting-process.md)。

此外，請檢閱的初始安裝或設定特定的常見問題清單：[安裝和升級的常見問題集](r/upgrade-and-installation-faq-sql-server-r-services.md)。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

## <a name="launchpad-issues"></a>啟動控制板問題

SQL Server 信任 Launchpad 服務管理的執行外部指令碼與 R、 Python 或其他外部執行階段通訊。 多個問題可以防止啟動控制板啟動，包括設定問題或變更，或遺漏網路通訊協定。

疑難排解程序的一部分，開始回答下列問題：

- 未啟動控制板永遠無法執行，或未停止運作？
- [啟動列] 正在執行哪些服務帳戶之下？
- Launchpad 服務帳戶有何種使用者權限？

### <a name="determine-whether-launchpad-is-running"></a>判斷是否正在執行 [啟動列]

1. 開啟**服務**面板 (Services.msc)。 或者，從命令列中，輸入**SQLServerManager13.msc**或**SQLServerManager14.msc**開啟[SQL Server 組態管理員](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 記下 [啟動列] 下執行的服務帳戶。 啟用 R 或 Python 每個執行個體應該有自己的 Launchpad 服務執行個體。 例如，具名執行個體的服務可能會類似_MSSQLLaunchpad$ InstanceName_。

3. 如果服務已停止，請將它重新啟動。 在重新啟動，如果有任何組態問題，訊息會發佈在系統事件記錄檔，而且服務已停止一次。 請檢查系統事件記錄檔，如需服務停止原因的詳細資訊。

4. 檢閱 RSetup.log 的內容，並確定在安裝程式中沒有任何錯誤。 例如，訊息*正在結束，代碼為 0*表示服務啟動失敗。

5. 若要尋找其他錯誤，檢閱 rlauncher.log 的內容。

### <a name="check-the-launchpad-service-account"></a>核取 [啟動列] 服務帳戶

預設服務帳戶可能是"NT 服務\$SQL2016 」 或 「 NT 服務\$SQL2017"。 最後一個部分可能會不同，根據您的 SQL 執行個體名稱。

Launchpad 服務 (Launchpad.exe) 會使用低權限的服務帳戶執行。 不過，若要啟動 R，並將 Python 和與資料庫執行個體進行通訊，啟動控制板服務帳戶需要下列的使用者權限：

- 以服務登入 (SeServiceLogonRight)
- 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)
- 略過跨越檢查 (SeChangeNotifyPrivilege)
- 調整處理序 (SeIncreaseQuotaSizePrivilege) 的記憶體配額

如需這些使用者權限資訊，請參閱中的 < Windows 權限和權限 > 一節[設定 Windows 服務帳戶與權限](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

> [!TIP]
> 如果您熟悉 SQL Server 診斷支援診斷平台 (SDP) 工具使用，您可以使用 SDP 名稱 MachineName_UserRights.txt 輸出檔案。

### <a name="review-launchpad-requirements"></a>檢閱 [啟動列] 的需求

任何幾個問題可以防止啟動控制板啟動。 Launchpad 服務可能會啟動，然後停止或損毀或服務可能會停止與連接逾時。 在這些情況下，系統通常已變更或設定為啟動控制板無法執行。

#### <a name="determine-whether-8dot3-notation-is-enabled"></a>判斷是否已啟用 8.3 標記法

使用 R 的相容性，SQL Server 2016 R 服務 （資料庫） 所需功能以支援使用短檔名建立的安裝所在的磁碟機*8.3 標記法*。 8.3 檔案名稱也稱為*短檔名*，是用來與 Microsoft Windows 或做為長檔名的替代方案的舊版本相容。

如果您要在其中安裝 R 的磁碟區不支援短檔名，啟動 從 SQL Server R 的處理程序可能無法找出正確的可執行檔，並將不會啟動 啟動列。

因應措施，您可以在安裝 SQL Server 和 R 服務安裝所在啟用磁碟區上的 8.3 標記法。 然後，您必須在 R Services 組態檔中提供工作目錄的簡短名稱。

1. 若要啟用 8.3 標記法，執行 fsutil 公用程式搭配*8dot3name*引數，如下所述： [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

2. 8.3 標記法啟用之後，開啟 RLauncher.config 檔案，並記下的屬性`WORKING_DIRECTORY`。 如需如何尋找此檔案相關資訊，請參閱[的機器學習疑難排解資料收集](data-collection-ml-troubleshooting-process.md)。

3. 使用 fsutil 公用程式，並*檔案*引數來指定 WORKING_DIRECTORY 中指定的資料夾的簡短檔案路徑。

4. 編輯組態檔來指定您在 WORKING_DIRECTORY 屬性中輸入的相同工作目錄。 或者，您可以指定不同的工作目錄，然後選擇 現有的路徑已存在相容 8.3 標記法。

> [!NOTE] 
> 未來的版本已經移除此限制。 如果您遇到此問題，請安裝下列其中一項：
> * SQL Server 2016 SP1 和 CU1: [for SQL Server 的累計更新 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)。
> * SQL Server 2016 RTM 累積更新 3，且這[hotfix](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3)，即可以視需要使用。

#### <a name="the-user-group-for-launchpad-cannot-log-on-locally"></a>啟動控制板的使用者群組無法在本機登入

在安裝期間的機器學習服務，SQL Server 建立的 Windows 使用者群組**SQLRUserGroup** ，然後使用 [啟動列] 來連接到 SQL Server 及執行外部指令碼作業所需的所有權限然後會佈建。 如果啟用此使用者群組時，它也會用來執行 Python 指令碼。

不過，在組織中限制更多的安全性原則強制執行的位置，此群組所需的權限可能已手動移除，或它們可能會自動撤銷原則。 如果已移除的權限，[啟動列] 無法連接到 SQL Server 和 SQL Server 無法呼叫外部執行階段。

若要修正此問題，請確定群組 **SQLRUserGroup** 擁有系統權限「允許本機登入」。

如需詳細資訊，請參閱[設定 Windows 服務帳戶與權限](https://msdn.microsoft.com/library/ms143504.aspx#Windows)。

#### <a name="improper-setup-leading-to-mismatched-dlls"></a>不正確的安裝程式導致不相符的 Dll

如果您與其他功能，補充程式在伺服器上，安裝資料庫引擎，然後再使用原始媒體稍後新增機器學習功能，可能會安裝的機器學習服務元件的版本錯誤。 當啟動控制板偵測到版本不相符時，它會關閉，並建立傾印檔案。

若要避免這個問題，請確定安裝在相同的修補程式層級的任何新功能與伺服器執行個體。

**若要升級錯誤的方式：**

1. 不使用 R 服務的 SQL Server 2016 安裝。
2. 升級 SQL Server 2016 累計更新 2。
3. 使用 RTM 媒體安裝 R 服務 （資料庫）。

**升級的正確方式：**

1. 不使用 R 服務的 SQL Server 2016 安裝。
2. 升級 SQL Server 2016 的所需的修補程式等級。 例如，安裝 Service Pack 1，然後累計更新 2。
3. 將功能加入正確的修補程式層級，執行 SP1 CU2 再次，安裝程式並選擇 R 服務 （資料庫）。 

#### <a name="check-whether-a-user-has-rights-to-run-external-scripts"></a>檢查使用者是否有權限才能執行外部指令碼

即使已正確設定 [啟動列]，它會傳回錯誤如果使用者沒有執行 R 或 Python 指令碼的權限。

如果您安裝 SQL Server 資料庫系統管理員身分，或您是資料庫擁有者，會自動授予此權限。 不過，其他使用者通常更有限權限。 如果使用者嘗試執行 R 指令碼，就會取得 [啟動列] 錯誤。

若要更正此問題，在 SQL Server Management Studio，安全性系統管理員可以修改 SQL 登入或 Windows 使用者帳戶執行下列指令碼：

```SQL
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

如需詳細資訊，請參閱[GRANT (TRANSACT-SQL](../t-sql/statements/grant-transact-sql.md)。

### <a name="common-launchpad-errors"></a>常見的 「 啟動列 」 錯誤

此區段會列出啟動控制板傳回的最常見錯誤訊息。

#### <a name="error-unable-to-launch-runtime-for-r-script"></a>錯誤：*無法啟動的 R 指令碼的執行階段*

如果 R 使用者 （也使用 Python） 的 Windows 群組無法登入執行 R Services 的執行個體，您可能會看到下列錯誤：

- 當您嘗試執行 R 指令碼產生的錯誤：

    * *無法啟動 'R' 指令碼的執行階段。請檢查 'R' 執行階段的組態。*

    * *發生外部指令碼錯誤。無法啟動執行階段。*

- 所產生的錯誤[!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)]服務：

    * *無法將啟動器 RLauncher.dll 初始化*

    * *未註冊任何啟動器 dll！*

    * *安全性記錄檔指出帳戶 NT 服務無法登入*

如需如何將必要的權限授與此使用者群組資訊，請參閱[安裝 SQL Server 2016 R Services](install/sql-r-services-windows-install.md)。

> [!NOTE]
> 如果您使用 SQL 登入從遠端工作站執行 R 指令碼，則不適用這項限制。

#### <a name="error-logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>錯誤：*登入失敗： 使用者未獲得要求的登入類型*

根據預設，[!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)]在啟動時，會使用下列帳戶： `NT Service\MSSQLLaunchpad`。 所設定的帳戶[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]安裝程式，以擁有所有必要的權限。

如果您將不同的帳戶指派給 [啟動列] 或 「 權限由 SQL Server 電腦上的原則移除，帳戶可能沒有必要的權限，您可能會看到這個錯誤：

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 登入失敗︰未授與使用者這個電腦所要求的登入類型。*

若要授與新的服務帳戶的必要權限，請使用本機安全性原則的應用程式，並更新包含下列權限的權限的帳戶：

+ 調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)
+ 略過跨越檢查 (SeChangeNotifyPrivilege)
+ 以服務登入 (SeServiceLogonRight)
+ 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)

#### <a name="error-unable-to-communicate-with-the-launchpad-service"></a>錯誤：*無法與 Launchpad 服務通訊*

如果您已安裝，然後再啟用 machine learning 中，但您會收到這個錯誤，當您嘗試執行 R 或 Python 指令碼時，就可能會執行已停止 Launchpad 服務執行個體。

1. 在 Windows 命令提示字元中，開啟 SQL Server 組態管理員。 如需詳細資訊，請參閱 [SQL Server 組態管理員](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 以滑鼠右鍵按一下執行個體的 SQL Server 啟動列，然後選取**屬性**。

3. 選取**服務**索引標籤，然後確認服務正在執行。 如果未執行，變更**啟動模式**至**自動**，然後選取**套用**。

4. 重新啟動服務時，通常可以修正問題，以便在機器學習指令碼執行。 如果重新啟動，仍無法解決問題，請記下的路徑中的引數**二進位路徑**屬性，然後執行下列動作：

    a. 檢閱啟動器的.config 檔案，並確定工作目錄無效。

    b. 請確定 [啟動列] 由 Windows 群組可以連接到 SQL Server 執行個體中所述[上一節](#bkmk_LaunchpadTS)。

    c. 如果您變更任何服務內容，請重新啟動啟動控制板服務。

#### <a name="error-fatal-error-creation-of-tmpfile-failed"></a>錯誤： *tmpFile 嚴重錯誤建立失敗*

在此案例中，您已成功安裝的機器學習功能，並執行 [啟動列]。 您嘗試執行一些簡單 R 或 Python 程式碼，但啟動失敗並發生錯誤，如下所示： 

>*無法與 R 指令碼的執行階段通訊。請檢查 R 執行階段的需求。*

同時，外部指令碼執行階段會當做 STDERR 訊息的一部分寫入下列訊息： 

>*嚴重錯誤： 建立 tmpfile 失敗。*

此錯誤表示嘗試啟動控制板使用的帳戶沒有登入資料庫的權限。 實作嚴格的安全性原則時，可能會發生這種情況。 若要判斷是否是這種情況，請檢閱 SQL Server 記錄檔，並檢查以查看是否在登入時遭拒 MSSQLSERVER01 帳戶。 R 的特定記錄檔中提供的相同資訊\_服務或 PYTHON\_服務。 尋找 ExtLaunchError.log。

根據預設，20 個帳戶設定，並透過 MSSQLSERVER20 名稱 MSSQLSERVER01 Launchpad.exe 處理程序相關聯上。 若要大量使用 R 或 Python，您可以增加帳戶數目。

若要解決此問題，請確定已針對群組*允許本機登入*機器學習功能已安裝並啟用的本機執行個體的權限。 在某些環境中，此權限層級可能需要向網路系統管理員的 GPO 例外狀況。

## <a name="r-script-issues"></a>R 指令碼問題

本章節包含 R 指令碼執行和 R 指令碼錯誤特有的一些常見問題。 清單不完整，因為有許多的 R 封裝，且錯誤可能會與不同版本之間的相同的 R 封裝。 我們建議您將 R 指令碼錯誤張貼上[Microsoft R Server 論壇](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR)，可支援機器學習中 R 服務 （資料庫內）、 Python、 Microsoft R 用戶端，與 Microsoft R 的機器學習服務使用的元件伺服器。

### <a name="multiple-r-instances-on-the-same-computer"></a>在相同電腦上的多個 R 執行個體

它可以很容易發現自己使用的同一部電腦中，R 的多個散發，以及相同的 R 封裝的多份不同的版本。 比方說，如果您安裝機器學習伺服器 （獨立） 和機器學習服務 （資料庫），安裝程式會建立不同的 R 程式庫的版本。 

當您嘗試從命令列執行指令碼，而且您不確定您使用的程式庫時，這類重複會成為問題。 或者，您可能會將套件安裝到錯誤的媒體櫃，然後稍後納悶為什麼找不到封裝從 SQL Server。

+ 請避免直接使用的 R 程式庫及工具，除了使用 SQL Server 執行個體的安裝，在某些限制狀況下，例如疑難排解或安裝新的封裝。 
+ 如果您需要使用 R 命令列工具，您可以安裝[Microsoft R 用戶端](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client)。 
+ SQL Server 提供 R 封裝的資料庫中的管理。 這是最簡單的方式來建立可在使用者之間共用的 R 封裝程式庫。 如需詳細資訊，請參閱[for SQL Server 的 R 封裝管理](r/r-package-management-for-sql-server-r-services.md)。

### <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>避免您在 SQL 計算內容中執行 R 時清除工作區

雖然您使用 R 主控台時，清除工作區是常見的它可以包含非預期的結果，在 SQL 計算內容。

`revoScriptConnection` 為包含從 SQL Server 呼叫 R 工作階段的相關資訊的 R 工作區中的物件。 不過，如果您的 R 程式碼會包含命令以清除工作區 (例如`rm(list=ls())`)，以及清除工作階段和 R 工作空間中的其他物件的所有資訊。

因應措施，避免任意清除變數和其他物件，您在 SQL Server 中執行 R 時。 您可以使用，以刪除特定變數**移除**函式：

```R
remove('name1', 'name2', ...)
```

如果有多個要刪除的變數，我們建議您將暫存變數的名稱儲存到清單，並在清單上執行定期記憶體回收。

### <a name="implied-authentication-for-remote-execution-via-odbc"></a>透過 ODBC 的遠端執行的隱含的驗證

如果您連接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]命令所使用的電腦來執行 R **RevoScaleR**函式，當您使用 ODBC 呼叫，將資料寫入到伺服器時，可能會發生錯誤。 只有當您使用 Windows 驗證時，就會發生此錯誤。

原因是針對 R 服務所建立的背景工作帳戶沒有權限可以連線到伺服器。 因此，無法代表您執行 ODBC 呼叫。 問題不會發生的 SQL 登入，因為具有 SQL 登入，認證會明確地從 R 用戶端至 ODBC SQL Server 執行個體，然後。 不過，使用 SQL 登入是安全性方面不如使用 Windows 驗證。

若要啟用您的 Windows 認證安全地傳遞已啟動遠端電腦上，SQL Server 指令碼必須模擬您的認證。 此程序稱為_隱含的驗證_。 若要這麼做，SQL Server 電腦執行 R 或 Python 指令碼的背景工作帳戶必須正確的權限。

1. 開啟[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]為您要執行 R 程式碼的執行個體的系統管理員。

2. 執行下列指令碼。 請務必編輯使用者群組名稱，如果您變更預設值，與電腦和執行個體名稱。

    ```SQL
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

### <a name="the-r-script-works-outside-of-t-sql-but-not-in-a-stored-procedure"></a>R 指令碼的運作 T-SQL 之外，但不是在預存程序

包裝之前 R 程式碼中的預存程序，最好在外部的 IDE，或其中一種 R 工具，例如 RTerm 或 RGui 執行 R 程式碼。 藉由使用這些方法，您可以測試和偵錯的程式藉由使用 r 會傳回詳細的錯誤訊息

不過，有時可完全外部 IDE 或公用程式中的程式碼可能無法在預存程序中執行，或在 SQL Server 計算內容。 如果發生這種情況，有各種問題之前，您可以假設封裝未搭配 SQL Server 中尋找。

1. 請檢查是否正在執行 [啟動列]。

2. 檢視訊息的輸入的資料或輸出資料是否包含具有不相容或不受支援的資料類型資料行。 例如，SQL database 的查詢通常會傳回 Guid 或 rowguids 的資料，都不支援。 如需詳細資訊，請參閱[R 程式庫和資料型別](r/r-libraries-and-data-types.md)。

3. 檢閱個別的 R 函數來判斷是否所有參數是否都支援 SQL Server 計算內容的 [說明] 頁。 ScaleR 的說明，請使用內嵌 R 說明命令，或參閱[封裝參考](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。

### <a name="you-get-different-results-from-the-same-script-when-running-in-sql-compared-to-other-environments"></a>在 SQL 相較於其他環境中執行時，從相同的指令碼取得不同的結果

R 指令碼可以在 SQL Server 內容中，傳回不同值有數種原因：

- SQL Server 與 r 之間傳遞資料時，某些資料類型上, 自動執行隱含類型轉換如需詳細資訊，請參閱[R 程式庫和資料型別](r/r-libraries-and-data-types.md)。

- 判斷是否位元是一項因素。 例如，通常在很 32 位元和 64 位元的浮動點 libraries 的數學運算的結果中的差異。

- 決定是否在任何作業中產生 Nan。 這會使失效的結果。

- 擷取對等的近於零的數字時，可以幅度加大小差異。

- 累積的捨入錯誤，可能會造成這類事件時小於零時，而非零的值。

### <a name="error-not-enough-quota-to-process-this-command"></a>錯誤：*配額不足，無法處理此命令*

這個錯誤可能表示其中一個步驟：

- 啟動控制板可能不足，無法執行外部查詢的外部使用者。 例如，如果您同時也會執行超過 20 個外部查詢，且僅有 20 個預設使用者，一個或多個查詢可能會失敗。

- 記憶體不足是可用來處理 R 工作。 會發生這個錯誤通常在預設環境中，SQL Server 可能正在使用的 70%的電腦的資源。 如需如何修改以支援更大的使用的資源 R 伺服器設定資訊，請參閱[運用您的 R 程式碼](r/operationalizing-your-r-code.md)。

### <a name="error-cant-find-package"></a>錯誤：*找不到封裝*

如果您在 SQL Server 中執行 R 程式碼並收到此訊息，但未取得訊息，當您在執行 SQL Server 外部相同的程式碼，則表示 SQL Server 所使用的預設程式庫位置未安裝的套件。

在許多方面，可能發生這個錯誤：

- 您在伺服器上，安裝新的封裝，但拒絕存取，因此使用者程式庫 R 已安裝的套件。

- 您安裝 R 服務，然後安裝其他的 R 工具或設定文件庫，包括 Microsoft R Server （獨立），Microsoft R 用戶端，RStudio、 等等。

若要判斷執行個體使用的 R 封裝文件庫的位置，開啟 SQL Server Management Studio （或任何其他資料庫查詢工具），連接到執行個體，然後再執行下列預存程序：

```SQL
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>範例結果

*STDOUT message(s) from external script:*

*[1] "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.SQL2016\\R_SERVICES"*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

若要解決此問題，您必須重新安裝至 SQL Server 執行個體文件庫套件。

>[!NOTE]
>如果您已升級使用 Microsoft R 最新版本的 SQL Server 2016 的執行個體，預設程式庫位置將會不同。 如需詳細資訊，請參閱[升級 R Services 的執行個體使用 SqlBindR](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="next-steps"></a>後續的步驟

[機器學習服務疑難排解和已知的問題](machine-learning-troubleshooting-faq.md)

[如需疑難排解機器學習的資料收集](data-collection-ml-troubleshooting-process.md)

[升級及安裝常見問題集](r/upgrade-and-installation-faq-sql-server-r-services.md)

[疑難排解 database engine 連接](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
