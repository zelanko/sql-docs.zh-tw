---
title: 啟動控制板服務和外部腳本執行的常見問題
ms.prod: sql
ms.technology: ''
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c90c59f3b59850bb0e2d1cf4cf40eb569e965eba
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715279"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>在 SQL Server 中啟動控制板服務和外部腳本的常見問題
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 信任的啟動控制板服務支援 R 和 Python 的外部腳本執行。 

多個問題可能會使啟動列無法啟動, 包括設定問題或變更, 或遺失網路通訊協定。 本文提供許多問題的疑難排解指引。 對於我們錯過的任何內容, 您可以將問題張貼到[Machine Learning Server 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR)。

## <a name="determine-whether-launchpad-is-running"></a>判斷啟動列是否正在執行

1. 開啟 [**服務**] 面板 (services.msc)。 或者, 在命令列中輸入**sqlservermanager13.msc**或**SQLServerManager14** , 以開啟[SQL Server 組態管理員](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 記下啟動控制板執行所在的服務帳戶。 啟用 R 或 Python 的每個實例都應該有自己的啟動列服務實例。 例如, 已命名實例的服務可能類似_MSSQLLaunchpad $ InstanceName_。

3. 如果服務已停止, 請將它重新開機。 在重新開機時, 如果設定發生任何問題, 系統事件記錄檔中會發佈一則訊息, 而服務會再次停止。 請檢查系統事件記錄檔, 以取得服務停止原因的詳細資料。

4. 請檢查 RSetup 的內容, 並確定安裝程式中沒有任何錯誤。 例如,*以代碼 0*結束的訊息表示服務無法啟動。

5. 若要尋找其他錯誤, 請檢查 rlauncher 的內容。

## <a name="check-the-launchpad-service-account"></a>檢查啟動列服務帳戶

預設服務帳戶可能是 "nt service\$SQL2016" 或 "nt service\$SQL2017"。 最後的部分可能有所不同, 視您的 SQL 實例名稱而定。

啟動列服務 (啟動列) 是使用低許可權服務帳戶來執行。 不過, 若要啟動 R 和 Python 並與資料庫實例通訊, 啟動列服務帳戶需要下列使用者權限:

- 以服務登入 (SeServiceLogonRight)
- 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)
- 略過跨越檢查 (SeChangeNotifyPrivilege)
- 調整進程的記憶體配額 (SeIncreaseQuotaSizePrivilege)

如需有關這些使用者權限的詳細資訊, 請參閱[設定 windows 服務帳戶和許可權](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)中的「windows 許可權與許可權」一節。

> [!TIP]
> 如果您熟悉 SQL Server 診斷使用支援診斷平臺 (SDP) 工具, 您可以使用 SDP 來檢查名為 MachineName_UserRights 的輸出檔。

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>啟動控制板的使用者群組無法在本機登入

在 Machine Learning 服務的安裝期間, SQL Server 會建立 Windows 使用者群組**SQLRUserGroup** , 然後以啟動控制板所需的擁有權限來進行布建, 以連接到 SQL Server 並執行外部腳本作業。 如果已啟用此使用者群組, 它也會用來執行 Python 腳本。

不過, 在強制執行更嚴格的安全性原則的組織中, 此群組所需的許可權可能已手動移除, 或原則可能會自動撤銷。 如果已移除許可權, 啟動列就無法再連接到 SQL Server, SQL Server 無法呼叫外部執行時間。

若要修正此問題，請確定群組 **SQLRUserGroup** 擁有系統權限「允許本機登入」。

如需詳細資訊，請參閱[設定 Windows 服務帳戶與權限](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

## <a name="permissions-to-run-external-scripts"></a>執行外部腳本的許可權

即使啟動列已正確設定, 如果使用者沒有執行 R 或 Python 腳本的許可權, 它會傳回錯誤。

如果您將 SQL Server 安裝為資料庫管理員, 或您是資料庫擁有者, 系統就會自動授與此許可權。 不過, 其他使用者通常會有較有限的許可權。 如果他們嘗試執行 R 腳本, 則會收到啟動列錯誤。

若要修正此問題, 在 SQL Server Management Studio 中, 安全性系統管理員可以執行下列腳本來修改 SQL 登入或 Windows 使用者帳戶:

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

如需詳細資訊, 請參閱[GRANT (transact-sql](../t-sql/statements/grant-transact-sql.md)。

## <a name="common-launchpad-errors"></a>常見的啟動控制板錯誤

本節列出啟動控制板傳回的最常見錯誤訊息。

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="unable-to-launch-runtime-for-r-script"></a>「無法啟動 R 腳本的執行時間」

如果 R 使用者的 Windows 群組 (也用於 Python) 無法登入正在執行 R Services 的實例, 您可能會看到下列錯誤:

- 當您嘗試執行 R 腳本時產生的錯誤:

    * *無法啟動 'R' 指令碼的執行階段。請檢查 'R' 執行階段的組態。*

    * *發生外部指令碼錯誤。無法啟動執行階段。*

- 服務所[!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)]產生的錯誤:

    * *無法將啟動器 RLauncher.dll 初始化*

    * *未註冊任何啟動器 dll！*

    * *安全性記錄指出帳戶 NT 服務無法登入*

如需有關如何授與此使用者群組必要許可權的詳細資訊, 請參閱[Install SQL Server R Services](install/sql-r-services-windows-install.md)。

> [!NOTE]
> 如果您使用 SQL 登入從遠端工作站執行 R 指令碼，則不適用這項限制。
::: moniker-end

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>「登入失敗: 使用者未被授與要求的登入類型」

根據預設, [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)]會在啟動時使用下列帳戶`NT Service\MSSQLLaunchpad`:。 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]安裝程式會設定此帳戶以擁有所有必要的許可權。

如果您將不同的帳戶指派給 [啟動列], 或 SQL Server 機上的原則移除該許可權, 則該帳戶可能沒有必要的許可權, 而您可能會看到此錯誤:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 登入失敗︰未授與使用者這個電腦所要求的登入類型。*

若要將必要的許可權授與新的服務帳戶, 請使用本機安全性原則應用程式, 並更新帳戶的許可權以包含下列許可權:

+ 調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)
+ 略過跨越檢查 (SeChangeNotifyPrivilege)
+ 以服務登入 (SeServiceLogonRight)
+ 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>「無法與啟動列服務通訊」

如果您已安裝並啟用機器學習, 但在嘗試執行 R 或 Python 腳本時收到此錯誤, 則實例的啟動列服務可能已停止執行。

1. 在 Windows 命令提示字元中，開啟 SQL Server 組態管理員。 如需詳細資訊，請參閱 [SQL Server 組態管理員](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 以滑鼠右鍵按一下實例的 [SQL Server Launchpad], 然後選取 [**屬性**]。

3. 選取 [**服務**] 索引標籤, 然後確認服務正在執行。 如果未執行, 請將 [**啟動模式]** 變更為 [**自動**],然後選取 [套用]。

4. 重新開機服務通常會修正問題, 讓機器學習服務腳本可以執行。 如果重新開機無法修正問題, 請注意 [**二進位路徑**] 屬性中的路徑和引數, 然後執行下列動作:

    a. 檢查啟動器的 .config 檔案, 並確定工作目錄有效。

    b. 確定 [啟動列] 所使用的 Windows 群組可以連接到 SQL Server 實例。

    c. 如果您變更任何服務屬性, 請重新開機啟動列服務。

## <a name="fatal-error-creation-of-tmpfile-failed"></a>「TmpFile 失敗建立嚴重錯誤」

在此案例中, 您已成功安裝機器學習功能, 且啟動控制板正在執行。 您嘗試執行一些簡單的 R 或 Python 程式碼, 但啟動列失敗並出現如下的錯誤: 

>*無法與 R 腳本的執行時間通訊。請檢查 R 執行時間的需求。*

同時, 外部腳本執行時間會將下列訊息寫入為 STDERR 訊息的一部分: 

>*嚴重錯誤: 建立 tmpfile 失敗。*

此錯誤表示啟動列嘗試使用的帳戶沒有登入資料庫的許可權。 執行嚴格的安全性原則時, 可能會發生這種情況。 若要判斷是否為這種情況, 請檢查 SQL Server 記錄, 並查看登入時是否拒絕 MSSQLSERVER01 帳戶。 在 R\_SERVICES 或 PYTHON\_服務特有的記錄中, 會提供相同的資訊。 尋找 ExtLaunchError。

根據預設, 系統會設定20個帳戶, 並與啟動列處理常式相關聯, 其名稱會透過 MSSQLSERVER20 MSSQLSERVER01。 如果您大量使用 R 或 Python, 您可以增加帳戶數目。

若要解決此問題, 請確定群組具有本機實例的 [*允許本機登*入] 許可權, 且已安裝並啟用機器學習功能。 在某些環境中, 此許可權層級可能需要來自網路系統管理員的 GPO 例外狀況。

## <a name="not-enough-quota-to-process-this-command"></a>「沒有足夠的配額可處理此命令」

此錯誤可能表示下列其中一項:

- 啟動列可能沒有足夠的外部使用者執行外部查詢。 例如, 如果您同時執行20個以上的外部查詢, 而且只有20個預設使用者, 則一或多個查詢可能會失敗。

- 記憶體不足, 無法處理 R 工作。 此錯誤最常在預設環境中發生, 其中 SQL Server 可能會使用最多 70% 的電腦資源。 如需有關如何修改伺服器設定以支援 R 更大的資源使用方式的詳細資訊, 請參閱[運用您的 r 程式碼](r/operationalizing-your-r-code.md)。

## <a name="cant-find-package"></a>「找不到封裝」

如果您在 SQL Server 中執行 R 程式碼, 並取得此訊息, 但未在 SQL Server 以外的程式碼時收到訊息, 則表示封裝未安裝到 SQL Server 所使用的預設程式庫位置。

此錯誤可能會以許多方式發生:

- 您已在伺服器上安裝新封裝, 但存取被拒, 因此 R 已將封裝安裝至使用者程式庫。

- 您已安裝 R Services, 然後安裝另一個 R 工具或一組程式庫, 包括 Microsoft R Server (獨立式)、Microsoft R Client、RStudio 等等。

若要判斷實例所使用之 R 封裝程式庫的位置, 請開啟 SQL Server Management Studio (或任何其他資料庫查詢工具), 連接到實例, 然後執行下列預存程式:

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>範例結果

*STDOUT message(s) from external script:*

*[1] "C:\\Program Files\\Microsoft SQL Server\\mssql13.mssqlserver。SQL2016\\R_SERVICES "*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

若要解決此問題, 您必須將封裝重新安裝到 SQL Server 實例程式庫。

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
>[!NOTE]
>如果您已將 SQL Server 2016 的實例升級為使用最新版的 Microsoft R, 則預設程式庫位置會不同。 如需詳細資訊, 請參閱[使用 SqlBindR 升級 R Services 的實例](install/upgrade-r-and-python.md)。
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>因為 Dll 不相符而關閉啟動列

如果您安裝具有其他功能的 database engine、修補伺服器, 然後稍後使用原始媒體來新增 Machine Learning 功能, 可能會安裝錯誤的 Machine Learning 元件版本。 當啟動列偵測到版本不相符時, 它會關閉並建立傾印檔案。

若要避免這個問題, 請務必在與伺服器實例相同的修補程式層級上安裝任何新功能。

**升級的錯誤方式:**

1. 安裝不含 R Services 的 SQL Server 2016。
2. 升級 SQL Server 2016 累計更新2。
3. 使用 RTM 媒體安裝 R Services (資料庫內)。

**升級的正確方式:**

1. 安裝不含 R Services 的 SQL Server 2016。
2. 將 SQL Server 2016 升級至所需的修補程式等級。 例如, 安裝 Service Pack 1 和累計更新2。
3. 若要在正確的修補程式等級新增功能, 請再次執行 SP1 並 CU2 安裝程式, 然後選擇 [R Services (資料庫內)]。 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>如果需要有8.3 標記法, 則啟動列失敗

> [!NOTE] 
> 在較舊的系統上, 如果有一個8.3 標記法需求, 啟動列就無法啟動。 此需求已在較新版本中移除。 SQL Server 2016 R 服務客戶應該安裝下列其中一項:
> * SQL Server 2016 SP1 和 CU1:[SQL Server 的累計更新 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)。
> * SQL Server 2016 RTM、累計更新3和此[修補程式](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), 視需要提供。

為了與 R 相容, SQL Server 2016 R Services (資料庫內) 需要安裝功能的磁片磁碟機, 以支援使用*8.3 標記法*來建立短檔案名。 8\.3 檔案名也稱為*簡短檔案名*, 用於與舊版 Microsoft Windows 的相容性, 或做為長檔名的替代方案。

如果您安裝 R 的磁片區不支援簡短檔案名, 從 SQL Server 啟動 R 的進程可能找不到正確的可執行檔, 且啟動列將不會啟動。

因應措施是, 您可以在安裝了 SQL Server 的磁片區上啟用8.3 標記法, 以及安裝 R Services 的位置。 然後，您必須在 R Services 組態檔中提供工作目錄的簡短名稱。

1. 若要啟用8.3 標記法, 請以*8dot3name*引數執行 fsutil 公用程式, 如這裡所述: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

2. 啟用8.3 標記法之後, 請開啟 RLauncher, 並記下的屬性`WORKING_DIRECTORY`。 如需如何尋找此檔案的詳細資訊, 請參閱[Machine Learning 疑難排解的資料收集](data-collection-ml-troubleshooting-process.md)。

3. 使用 fsutil 公用程式搭配*file*引數, 為 WORKING_DIRECTORY 中指定的資料夾指定簡短的檔案路徑。

4. 編輯設定檔, 以指定您在 WORKING_DIRECTORY 屬性中輸入的相同工作目錄。 或者, 您也可以指定不同的工作目錄, 然後選擇已經與8.3 標記法相容的現有路徑。
::: moniker-end

## <a name="next-steps"></a>後續步驟

[Machine Learning Services 疑難排解和已知問題](machine-learning-troubleshooting-faq.md)

[用於疑難排解機器學習服務的資料收集](data-collection-ml-troubleshooting-process.md)

[升級及安裝常見問題集](r/upgrade-and-installation-faq-sql-server-r-services.md)

[資料庫引擎連接疑難排解](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
