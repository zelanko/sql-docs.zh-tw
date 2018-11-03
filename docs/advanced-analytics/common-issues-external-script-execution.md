---
title: Launchpad 服務和 SQL Server 中的外部指令碼執行常見 |Microsoft Docs
ms.prod: sql
ms.technology: mlserver
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b480c400ae2068bb6701192e77d97672ddeb024e
ms.sourcegitcommit: b29745051be2326268f165cf72f5eb95dc893564
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/31/2018
ms.locfileid: "50254444"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>Launchpad 服務與 SQL Server 中的外部指令碼執行的一般問題
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 SQL Server 受信任的 Launchpad 服務支援 R 和 Python 的外部指令碼執行。 在 SQL Server 2016 R Services，SP1 會提供服務。 SQL Server 2017 包含一直安裝一部分啟動控制板 ervice。

多個問題可能會妨礙 Launchpad 啟動、 包括設定問題或進行變更，或遺漏的網路通訊協定。 這篇文章提供許多問題的疑難排解的指引。 任何我們錯過了，您可以張貼問題[Machine Learning Server 論壇](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR)。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 Machine Learning 服務

## <a name="determine-whether-launchpad-is-running"></a>判斷是否正在執行啟動控制板

1. 開啟**Services**面板 (Services.msc)。 或者，您也可以從命令列中，輸入**SQLServerManager13.msc**或是**SQLServerManager14.msc**以開啟[SQL Server 組態管理員](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 請記下執行 Launchpad 服務帳戶。 啟用 R 或 Python 每個執行個體應該擁有自己的 Launchpad 服務執行個體。 比方說，具名執行個體的服務可能會類似_MSSQLLaunchpad$ InstanceName_。

3. 如果服務已停止，請將它重新啟動。 在重新啟動，如果有任何問題的組態，訊息會發佈在系統事件記錄檔，而且服務已停止一次。 請檢查系統事件記錄檔，如需詳細資訊，關於服務停止的原因。

4. 檢閱 RSetup.log 的內容，並確定在安裝程式沒有任何錯誤。 例如，訊息*結束，代碼為 0*表示服務啟動失敗。

5. 若要尋找其他錯誤，請檢閱 rlauncher.log 的內容。

## <a name="check-the-launchpad-service-account"></a>核取 Launchpad 服務帳戶

預設服務帳戶可能是"NT Service\$SQL2016 」 或 「 NT 服務\$SQL2017"。 最後一個部分可能會有所不同，視您的 SQL 執行個體名稱。

Launchpad 服務 (Launchpad.exe) 會使用低權限的服務帳戶執行。 不過，若要啟動 R 和 Python，並與資料庫執行個體通訊，Launchpad 服務帳戶需要下列的使用者權限：

- 以服務登入 (SeServiceLogonRight)
- 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)
- 略過跨越檢查 (SeChangeNotifyPrivilege)
- 調整處理序 (SeIncreaseQuotaSizePrivilege) 的記憶體配額

如需這些使用者權限的詳細資訊，請參閱中的 < Windows 權限和權限 > 一節[設定 Windows 服務帳戶與權限](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

> [!TIP]
> 如果您熟悉的 SQL Server 診斷使用支援診斷平台 (SDP) 工具，您可以使用 SDP 同名 MachineName_UserRights.txt 輸出檔案。

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>Launchpad 的使用者群組不能在本機登入

在安裝期間的 Machine Learning 服務，SQL Server 建立的 Windows 使用者群組**SQLRUserGroup** ，然後將它佈建具備所有權限所需的啟動列來連線到 SQL Server 及執行外部指令碼作業。 如果啟用此使用者群組時，它也會用來執行 Python 指令碼。

不過，在組織中實施更嚴格的安全性原則，此群組所需的權限可能已手動移除，或它們可能會自動被原則撤銷。 如果已移除的權限，Launchpad 不再可以連線到 SQL Server 和 SQL Server 無法呼叫外部執行階段。

若要修正此問題，請確定群組 **SQLRUserGroup** 擁有系統權限「允許本機登入」。

如需詳細資訊，請參閱 <<c0> [ 設定 Windows 服務帳戶與權限](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

## <a name="permissions-to-run-external-scripts"></a>若要執行外部指令碼的權限

即使已正確設定 [啟動列]，如果使用者沒有權限來執行 R 或 Python 指令碼會傳回錯誤。

如果您安裝 SQL Server 資料庫系統管理員身分，或您是資料庫擁有者，您會自動授與此權限。 不過，其他使用者通常有更多限制的權限。 如果使用者嘗試執行 R 指令碼時，他們會取得的啟動列 」 錯誤。

若要更正此問題，在 SQL Server Management Studio，安全性系統管理員可以修改 SQL 登入或 Windows 使用者帳戶執行下列指令碼：

```SQL
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

如需詳細資訊，請參閱 <<c0> [ 授與 (Transact SQL](../t-sql/statements/grant-transact-sql.md)。

## <a name="common-launchpad-errors"></a>Launchpad 的常見錯誤

此區段會列出最常見的錯誤訊息，Launchpad 會傳回。

## <a name="unable-to-launch-runtime-for-r-script"></a>「 無法啟動 R 指令碼的執行階段 」

如果 Windows 群組的 R 使用者 （也用於 Python） 無法登入執行 R Services 的執行個體，您可能會看到下列錯誤：

- 當您嘗試執行 R 指令碼產生的錯誤：

    * *無法啟動 'R' 指令碼的執行階段。請檢查 'R' 執行階段的組態。*

    * *發生外部指令碼錯誤。無法啟動執行階段。*

- 所產生的錯誤[!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)]服務：

    * *無法將啟動器 RLauncher.dll 初始化*

    * *未註冊任何啟動器 dll！*

    * *安全性記錄檔指出帳戶 NT 服務無法登入*

如需如何將必要的權限授與此使用者群組的資訊，請參閱[安裝 SQL Server 2016 R Services](install/sql-r-services-windows-install.md)。

> [!NOTE]
> 如果您使用 SQL 登入從遠端工作站執行 R 指令碼，則不適用這項限制。

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>「 登入失敗： 使用者未獲得所要求的登入類型 」

根據預設，[!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)]在啟動時使用下列帳戶： `NT Service\MSSQLLaunchpad`。 帳戶蒻謔[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]安裝程式，以擁有所有必要的權限。

如果您將不同的帳戶指派給 Launchpad，或在 SQL Server 電腦上的原則移除了，帳戶可能沒有必要的權限，以及您可能會看到此錯誤：

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 登入失敗︰未授與使用者這個電腦所要求的登入類型。*

若要授與新的服務帳戶的必要權限，請使用本機安全性原則的應用程式，並更新帳戶權限，以包含下列權限：

+ 調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)
+ 略過跨越檢查 (SeChangeNotifyPrivilege)
+ 以服務登入 (SeServiceLogonRight)
+ 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>「 無法與 Launchpad 服務通訊 」

如果您已安裝並啟用機器學習服務，但當您嘗試執行 R 或 Python 指令碼時，您會收到這個錯誤，就可能會執行已停止執行個體的 Launchpad 服務。

1. 在 Windows 命令提示字元中，開啟 SQL Server 組態管理員。 如需詳細資訊，請參閱 [SQL Server 組態管理員](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 以滑鼠右鍵按一下執行個體的 SQL Server 啟動控制板，然後選取**屬性**。

3. 選取 **服務**索引標籤，然後確認 確認服務正在執行。 如果未執行，變更**Startmode**來**自動**，然後選取**套用**。

4. 重新啟動服務時，通常可以修正問題，以便在機器學習服務指令碼執行。 如果重新啟動操作無法解決此問題，請注意路徑中的引數**二進位路徑**屬性，然後執行下列動作：

    A. 檢閱啟動程式的.config 檔案，並確定工作目錄無效。

    B. 請確定 launchpad 所使用的 Windows 群組可以連接到 SQL Server 執行個體中所述[上一節](#bkmk_LaunchpadTS)。

    c. 如果您變更任何的服務屬性，請重新啟動 Launchpad 服務。

## <a name="fatal-error-creation-of-tmpfile-failed"></a>「 嚴重錯誤 tmpFile 建立失敗 」

在此案例中，您已成功安裝機器學習服務功能，且 Launchpad 正在執行。 您嘗試執行一些簡單 R 或 Python 程式碼，但 Launchpad 失敗並發生錯誤，如下所示： 

>*無法與 R 指令碼的執行階段通訊。請檢查 R 執行階段的需求。*

在此同時，外部指令碼執行階段會將下列訊息寫入 STDERR 訊息的一部分： 

>*嚴重錯誤： 建立 tmpfile 失敗。*

此錯誤表示 Launchpad 正在嘗試使用的帳戶沒有登入資料庫的權限。 當實作嚴格的安全性原則時，可能會發生這種情況。 若要判斷這是否的情況下，檢閱 SQL Server 記錄檔，並檢查以查看在登入時是否被拒 MSSQLSERVER01 帳戶。 R 特定的記錄檔中會提供相同的資訊\_服務或 PYTHON\_服務。 ExtLaunchError.log 外觀。

根據預設，會設定 20 個帳戶，並將其名稱 MSSQLSERVER01 透過 MSSQLSERVER20 Launchpad.exe 處理程序相關聯中。 若要大量使用 R 或 Python，您可以增加帳戶數目。

若要解決此問題，請確定群組具有*允許本機登入*機器學習服務功能已安裝並啟用的本機執行個體的權限。 在某些環境中，此權限等級可能會需要網路系統管理員從 GPO 例外狀況。

## <a name="not-enough-quota-to-process-this-command"></a>「 配額不足以執行此命令 」

此錯誤可能表示其中一個步驟：

- Launchpad 可能不足以執行外部查詢的外部使用者。 例如，如果您同時也會執行超過 20 個外部查詢，且僅有 20 個預設使用者，一個或多個查詢可能會失敗。

- 沒有足夠的記憶體可處理的 R 工作。 會發生這個錯誤通常在預設環境中，SQL Server 可能會使用的最多 70%的電腦資源。 如需如何修改伺服器組態，以支援更大用處 R 的資源資訊，請參閱[運用您的 R 程式碼](r/operationalizing-your-r-code.md)。

## <a name="cant-find-package"></a>「 找不到套件 」

如果您在 SQL Server 中執行 R 程式碼並收到這個訊息，但未取得訊息，當您執行相同 SQL Server 外部的程式碼，表示封裝未安裝 SQL Server 所使用的預設程式庫位置。

在許多方面，就會發生此錯誤：

- 您的伺服器上，安裝新的封裝但存取被拒，所以 R 使用者程式庫來安裝封裝。

- 您已安裝 R Services 並再安裝其他 R 工具或文件庫，包括 Microsoft R Server （獨立式），Microsoft R Client，RStudio、 設定等等。

若要判斷執行個體使用的 R 套件程式庫的位置，開啟 SQL Server Management Studio （或任何其他的資料庫查詢工具），連接到執行個體，然後再執行下列預存程序：

```SQL
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>範例結果

*STDOUT message(s) from external script:*

*[1]"c:\\程式檔案\\Microsoft SQL Server\\MSSQL13。SQL2016\\R_SERVICES"*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

若要解決此問題，您必須重新安裝 SQL Server 執行個體文件庫封裝。

>[!NOTE]
>如果您已升級的 SQL Server 2016，以便使用最新版的 Microsoft R 執行個體，預設程式庫位置將會不同。 如需詳細資訊，請參閱 <<c0> [ 使用 SqlBindR 升級 R Services 的執行個體](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>啟動控制板因不相符的 Dll 而關閉

如果您與其他功能，補充程式伺服器上，安裝 database engine，然後使用原始媒體，稍後再新增機器學習服務功能，就可能安裝的機器學習服務元件的版本錯誤。 當啟動控制板偵測到版本不相符時，它會關閉，並建立傾印檔案。

若要避免這個問題，請務必安裝任何新的功能，在相同的修補程式層級與伺服器執行個體。

**若要升級錯誤的方式：**

1. 安裝不含 R Services 的 SQL Server 2016。
2. 升級 SQL Server 2016 累積更新 2。
3. 使用 RTM 媒體來安裝 R Services （資料庫）。

**升級的正確方式：**

1. 安裝不含 R Services 的 SQL Server 2016。
2. 升級 SQL Server 2016 所需的修補程式等級。 例如，安裝 Service Pack 1，然後累計更新 2。
3. 將功能新增正確的修補程式層級中，執行 SP1 CU2 再次，安裝程式並選擇 R Services （資料庫）。 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>無法啟動 8.3 標記法是否需要啟動控制板

> [!NOTE] 
> 較舊的系統上，啟動控制板可以無法啟動 8.3 標記法需求時。 更新的版本中已移除這項需求。 SQL Server 2016 R Services 的客戶應該安裝下列其中一項：
> * SQL Server 2016 SP1 和 CU1:[適用於 SQL Server 的累計更新 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)。
> * SQL Server 2016 RTM、 累計更新 3 和這[hotfix](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3)，這是隨選點播。

使用 R 的相容性，SQL Server 2016 R Services （資料庫內） 所需功能以支援使用短檔名建立的安裝所在的磁碟機*8.3 標記法*。 8.3 檔案名稱也稱為*短檔名*，並且用於與 Microsoft Windows 或長檔名的替代方案的舊版相容。

如果您要在其中安裝 R 的磁碟區不支援短檔名，從 SQL Server 啟動 R 的處理程序可能無法找出正確的可執行檔，並將不會啟動 [啟動列]。

因應措施，您可以在安裝 SQL Server 和 R 服務的安裝位置啟用 8.3 標記法，磁碟區上。 然後，您必須在 R Services 組態檔中提供工作目錄的簡短名稱。

1. 若要啟用 8.3 標記法，執行 fsutil 公用程式搭配*8dot3name*如下所述的引數： [fsutil 8dot3name （英文)](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

2. 啟用 8.3 標記法後，開啟 RLauncher.config 檔案，並記下的 屬性`WORKING_DIRECTORY`。 如需如何尋找此檔案相關資訊，請參閱[機器學習服務疑難排解的資料收集](data-collection-ml-troubleshooting-process.md)。

3. 使用 fsutil 公用程式，並*檔案*引數來指定 WORKING_DIRECTORY 中指定的資料夾簡短檔案路徑。

4. 編輯組態檔來指定 WORKING_DIRECTORY 屬性中輸入的相同工作目錄。 或者，您可以指定不同的工作目錄，並選擇已與 8.3 標記法相容的現有路徑。


## <a name="next-steps"></a>後續步驟

[機器學習服務疑難排解和已知的問題](machine-learning-troubleshooting-faq.md)

[疑難排解 機器學習服務的資料收集](data-collection-ml-troubleshooting-process.md)

[升級及安裝常見問題集](r/upgrade-and-installation-faq-sql-server-r-services.md)

[疑難排解 database engine 連接](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
