---
title: 疑難排解 Launchpad 服務的問題
description: 本文提供疑難排解指南，幫助您解決包括設定問題或變更，或是遺失網路通訊協定等等，會導致 SQL Server Trusted Launchpad 服務無法啟動的問題。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/30/2019
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e814e135c7e7054231aea3988a30afe755e1fc9d
ms.sourcegitcommit: 04fb4c2d7ccddd30745b334b319d9d2dd34325d6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/09/2020
ms.locfileid: "89570284"
---
# <a name="troubleshoot-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>疑難排解 Launchpad 服務以及在 SQL Server 中執行外部指令碼的問題
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

本文提供有關 SQL Server Trusted Launchpad 服務問題的疑難排解指南。 Launchpad 服務支援 R 與 Python 執行外部指令碼。 包括設定問題或變更，或是遺失網路通訊協定等等的許多問題都可能會使啟動控制板無法啟動。  

## <a name="determine-whether-launchpad-is-running"></a>判斷啟動控制板是否在執行中

1. 開啟 [服務]  面板 (Services.msc)。 或者，從命令列中輸入 **SQLServerManager13.msc** 或 **SQLServerManager14.msc**，以開啟 [SQL Server 組態管理員](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 記下用於執行啟動控制板的服務帳戶。 已啟用 R 或 Python 的每個執行個體都應該有自己的啟動控制板服務執行個體。 例如，具名執行個體的服務可能會類似 _MSSQLLaunchpad$InstanceName_。

3. 如果服務已停止，請將它重新啟動。 重新啟動時，如果設定發生任何問題，會在系統事件記錄檔中發佈一則訊息，而服務會再次停止。 請檢查系統事件記錄檔，以取得服務停止原因的詳細資料。

4. 請檢閱 RSetup.log 的內容，並確定安裝程式中沒有任何錯誤。 例如，*正在結束，錯誤碼為 0*指示服務啟動失敗。

5. 若要尋找其他錯誤，請檢查 rlauncher.log 的內容。

## <a name="check-the-launchpad-service-account"></a>檢查啟動控制板服務帳戶

預設服務帳戶可能是 "NT Service\$SQL2016" 或 "NT Service\$SQL2017"。 最後的部分可能會有所不同，視您的 SQL 執行個體名稱而定。

啟動控制板服務 (Launchpad.exe) 會使用低權限服務帳戶來執行。 不過，若要啟動 R 和 Python 並與資料庫執行個體通訊，啟動控制板服務帳戶需要下列使用者權限：

- 以服務登入 (SeServiceLogonRight)
- 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)
- 略過跨越檢查 (SeChangeNotifyPrivilege)
- 調整處理序的記憶體配額 (SeIncreaseQuotaSizePrivilege)

如需這些使用者權限的詳細資訊，請參閱[設定 Windows 服務帳戶和權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 中的「Windows 權限和權利」一節。

> [!TIP]
> 如果您熟悉如何使用支援診斷平臺 (SDP) 工具進行 SQL Server 診斷，可以使用 SDP 來檢閱名稱為 MachineName_UserRights.txt 的輸出檔。

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>啟動控制板的使用者群組無法在本機登入

在機器學習服務安裝期間，SQL Server 會建立 Windows 使用者群組 **SQLRUserGroup**，然後會為它佈建啟動控制板連接至 SQL Server 及執行外部指令碼作業所需的所有權限。 如果已啟用此使用者群組，系統也會用它來執行 Python 指令碼。

不過，在強制執行更嚴格安全性原則的組織中，此群組所需的權限可能會被手動移除，或是自動被原則撤銷。 如果權限已遭到移除，啟動控制板就無法再連線到 SQL Server，而 SQL Server 也無法呼叫外部執行階段。

若要修正此問題，請確定群組 **SQLRUserGroup** 擁有系統權限「允許本機登入」  。

如需詳細資訊，請參閱[設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

## <a name="permissions-to-run-external-scripts"></a>執行外部指令碼的權限

即使啟動控制板已正確設定，如果使用者沒有執行 R 或 Python 指令碼的權限，控制板就會傳回錯誤。

如果將 SQL Server 安裝為資料庫管理員，或您是資料庫擁有者，就會被自動授與此權限。 不過，其他使用者通常會擁有限制較多的權限。 如果他們嘗試執行 R 指令碼，會收到啟動控制板錯誤。

若要修正此問題，在 SQL Server Management Studio 中，安全性系統管理員可以執行下列指令碼來修改 SQL 登入或 Windows 使用者帳戶：

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

如需詳細資訊，請參閱 [GRANT (Transact-SQL](../../t-sql/statements/grant-transact-sql.md)。

## <a name="common-launchpad-errors"></a>常見的啟動控制板錯誤

本節列出啟動控制板所傳回的最常見錯誤訊息。

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="unable-to-launch-runtime-for-r-script"></a>「無法啟動 R 指令碼的執行階段」

如果 R 使用者的 Windows 群組 (也用於 Python) 無法登入正在執行 R Services 的執行個體，您可能會看到下列錯誤：

- 當您嘗試執行 R 指令碼時產生的錯誤：

    * *無法啟動 'R' 指令碼的執行階段。請檢查 'R' 執行階段的組態。*

    * *發生外部指令碼錯誤。無法啟動執行階段。*

- [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務產生的錯誤：

    * *無法將啟動器 RLauncher.dll 初始化*

    * *未註冊任何啟動器 dll！*

    * *安全性記錄檔指出帳戶 NT SERVICE 無法登入*

如需如何授與此使用者群組必要權限的資訊，請參閱[安裝 SQL Server R Services](../install/sql-r-services-windows-install.md)。

> [!NOTE]
> 如果您使用 SQL 登入從遠端工作站執行 R 指令碼，則不適用這項限制。
::: moniker-end

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>「登入失敗︰未授與使用者所要求的登入類型」

根據預設，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 會在啟動時使用以下帳戶：`NT Service\MSSQLLaunchpad`。 它是由 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝程式設定，以取得所有必要權限。

如果您將不同的帳戶指派給 Launchpad，或 SQL Server 電腦上的原則移除了權限，帳戶就可能沒有必要的權限，而您可能會看到此錯誤：

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 登入失敗︰未授與使用者這個電腦所要求的登入類型。*

若要將必要權限授與新的服務帳戶，請使用本機安全性原則應用程式，並更新帳戶權限以包含下列權限︰

+ 調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)
+ 略過跨越檢查 (SeChangeNotifyPrivilege)
+ 以服務登入 (SeServiceLogonRight)
+ 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>「無法與 Launchpad 服務通訊」

如果您已經安裝並啟用機器學習服務，但在嘗試執行 R 或 Python 指令碼時發生此錯誤，表示執行個體的啟動控制板服務已經停止執行。

1. 在 Windows 命令提示字元中，開啟 SQL Server 組態管理員。 如需詳細資訊，請參閱 [SQL Server 組態管理員](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 以滑鼠右鍵按一下執行個體的 SQL Server 啟動控制板，然後選取 [屬性]  。

3. 選取 [服務]  索引標籤，然後確認服務正在執行。 如果沒有執行，請將 [啟動模式]  變更為 [自動]  ，然後選取 [套用]  。

4. 重新啟動服務通常會修正問題，讓機器學習服務指令碼可以執行。 如果重新啟動無法修正問題，請記下 [二進位路徑]  屬性中的路徑和引數，然後執行以下動作：

    a. 檢閱 launcher 的 .config 檔案，並確定工作目錄是有效的。

    b. 確定啟動控制板使用的 Windows 群組能夠連線到 SQL Server 執行個體。

    c. 如果您對服務屬性進行任何變更，請重新啟動啟動控制板服務。

## <a name="fatal-error-creation-of-tmpfile-failed"></a>「發生嚴重錯誤：TmpFile 建立失敗」

在此案例中，您已成功安裝機器學習服務功能，且啟動控制板正在執行中。 您嘗試執行一些簡單的 R 或 Python 程式碼，但啟動控制板失敗並發生如下所示的錯誤： 

>「無法與 R 指令碼的執行階段通訊。  請檢查 R 執行階段的需求。」

同時，外部指令碼執行階段會將以下訊息寫入為 STDERR 訊息的一部分： 

>「發生嚴重錯誤：TmpFile 建立失敗。」 

此錯誤指示啟動控制板嘗試使用的帳戶沒有登入資料庫的權限。 實作嚴格的安全性原則時，可能會發生此情況。 若要判斷是否是這種情形，請檢閱 SQL Server 記錄，並查看 MSSQLSERVER01 帳戶是否在登入時遭到拒絕。 R\_SERVICES 或 PYTHON\_SERVICES 特定的記錄中提供了相同資訊。 尋找 ExtLaunchError.log。

根據預設，系統會設定 20 個帳戶，並與 Launchpad.exe 處理序建立關聯，分別命名為 MSSQLSERVER01 至 MSSQLSERVER20。 如果您大量使用 R 或 Python，可以增加帳戶數目。

若要解決此問題，請確定群組具備已安裝並啟用機器學習服務功能的本機實例「允許本機登入」  權限。 在某些環境中，此權限等級可能需要來自網路系統管理員的 GPO 例外狀況。

## <a name="not-enough-quota-to-process-this-command"></a>「沒有足夠的配額可處理此命令」

此錯誤可能具有下列其中一項意義：

- 啟動控制板可能沒有足夠的外部使用者能夠執行外部查詢。 例如，如果您同時執行 20 個以上的外部查詢，而且只有 20 個預設使用者，就可能會有一或多個查詢失敗。

- 記憶體不足，無法處理 R 工作。 此錯誤最常在預設環境中發生，其中 SQL Server 可能會使用多達 70% 的電腦資源。 如需有關如何修改伺服器設定以支援讓 R 能夠使用更多資源的詳細資訊，請參閱[運用 R 程式碼](../r/operationalizing-your-r-code.md)。

## <a name="cant-find-package"></a>「找不到封裝嗎」

如果此訊息在您於 SQL Server 中執行 R 程式碼時出現，但在 SQL Server 外部執行相同程式碼時並未出現，表示封裝並未安裝到 SQL Server 所使用的預設程式庫位置。

此錯誤可能會以多種方式發生：

- 您已在伺服器上安裝新封裝，但存取被拒，因此 R 已將封裝安裝至使用者程式庫。

- 您已安裝 R Services，然後安裝另一個 R 工具或一組程式庫，包括 Microsoft R Server (獨立式)、Microsoft R Client、RStudio 等等。

若要判斷執行個體所使用 R 封裝程式庫的位置，請開啟 SQL Server Management Studio (或任何其他資料庫查詢工具)，連線到執行個體，然後執行以下預存程序：

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>範例結果

*STDOUT message(s) from external script:*

*[1] "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.SQL2016\\R_SERVICES"*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

若要解決此問題，必須將封裝重新安裝到 SQL Server 執行個體程式庫。

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
>[!NOTE]
>如果您已將 SQL Server 2016 的執行個體升級為使用最新版的 Microsoft R，預設程式庫位置會不同。 如需詳細資訊，請參閱[使用 SqlBindR 升級 R Services 的執行個體](../install/upgrade-r-and-python.md)。
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>啟動控制板因 DLL 不相符而關閉

如果您安裝具有其他功能的資料庫引擎、修補伺服器，然後稍後使用原始媒體來新增機器學習服務功能，可能會安裝錯誤版本的的機器學習服務元件。 當啟動控制板偵測到版本不符時，它會關閉並建立一個傾印檔案。

若要避免這個問題，請務必在與伺服器執行個體相同的修補程式等級安裝任何新功能。

**錯誤的升級方式：**

1. 安裝不含 R Services 的 SQL Server 2016。
2. 升級 SQL Server 2016 累積更新 2。
3. 使用 RTM 媒體安裝 R Services (資料庫內)。

**正確的升級方式：**

1. 安裝不含 R Services 的 SQL Server 2016。
2. 將 SQL Server 2016 升級至所需的修補程式等級。 例如，安裝 Service Pack 1，然後安裝累積更新 2。
3. 若要在正確的修補程式等級新增功能，請再次執行 SP1 和 CU2 安裝程式，然後選擇 R Services (資料庫內)。 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>如果需要 8.3 標記法，啟動控制板會無法啟動

> [!NOTE] 
> 在較舊的系統上，如果有一個 8.3 標記法需求，啟動控制板可能會無法啟動。 較新的版本已移除此需求。 SQL Server 2016 R Services 客戶應該安裝下列其中一項：
> * SQL Server 2016 SP1 和 CU1：[SQL Server 的累積更新 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)。
> * SQL Server 2016 RTM、累積更新 3，和此 [hotfix](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3) (在要求時提供)。

針對與 R 的相容性，SQL Server 2016 R Services (資料庫內) 要求安裝功能的磁碟機必須支援使用「8.3 標記法」  建立短檔名。 8\.3 檔案名稱也稱為「短檔名」  ，並用於提供與舊版 Microsoft Windows 的相容性，或作為長檔名的替代項目。

如果您安裝 R 的磁碟區不支援短檔名，從 SQL Server 啟動 R 的處理序可能會無法找出正確的可執行檔，且啟動控制板也不會啟動。

因應措施是，您可以在 SQL Server 和 R Services 安裝所在的磁碟區上啟用 8.3 標記法。 然後，您必須在 R Services 組態檔中提供工作目錄的簡短名稱。

1. 若要啟用 8.3 標記法，請執行 fsutil 公用程式配合 *8dot3name* 引數，如下所示︰[fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

2. 啟用 8.3 標記法後，開啟 RLauncher.config 檔案並記下 `WORKING_DIRECTORY` 的屬性。 如需如何尋找此檔案的詳細資訊，請參閱[機器學習服務資料收集疑難排解](data-collection-ml-troubleshooting-process.md)。

3. 使用 fsutil 公用程式搭配 *file* 引數來指定 WORKING_DIRECTORY 中所指定的資料夾簡短檔案路徑。

4. 編輯設定檔，以指定您在 WORKING_DIRECTORY 屬性中輸入的相同工作目錄。 或者，您可以指定不同的工作目錄，以及選擇已經與 8.3 標記法相容的現有路徑。
::: moniker-end

## <a name="next-steps"></a>後續步驟

[機器學習服務疑難排解和已知問題](machine-learning-troubleshooting-overview.md)

[用於針對機器學習進行疑難排解所收集的資料](data-collection-ml-troubleshooting-process.md)

[安裝 SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md)

[針對資料引擎連線進行疑難排解](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
