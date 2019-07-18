---
title: 安裝 R Server 或 Machine Learning Server （獨立式） 使用 SQL Server 安裝程式-SQL Server Machine Learning
description: 安裝程式使用 RevoScaleR、 revoscalepy、 MicrosoftML 及其他套件的 R 和 Python 開發的執行個體感知的獨立機器學習服務伺服器。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f721a840b6fba4a840484fccb1cafb334b1ba438
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962850"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>安裝 Machine Learning Server （獨立式） 或使用 SQL Server 安裝的 R Server （獨立式）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 安裝程式包含**共用的功能**非感知執行個體，安裝選項執行 SQL Server 外部的獨立 machine learning 伺服器。 在 SQL Server 2016 中，這項功能稱為**R Server （獨立式）** 。 在 SQL Server 2017 中，它會呼叫**Machine Learning Server （獨立式）** ，其中包括 R 和 Python。 

為 SQL Server 安裝程式已安裝在獨立伺服器和非 SQL 品牌版本的功能上相當[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，支援相同的使用案例和案例，包括：

+ 遠端執行，在同一個主控台中的本機和遠端工作階段之間切換
+ 使用 web 節點和計算節點的運算化
+ Web 服務部署： 若要封裝到 web 服務的 R 和 Python 指令碼的能力
+ 完整的 R 和 Python 函式程式庫

與 SQL Server 分離的獨立伺服器，為 R 和 Python 環境的設定，保護及存取使用的基礎作業系統和獨立伺服器，而不是 SQL Server 中提供的工具。

作為 SQL Server 的輔助，獨立伺服器是很有用，如果您要開發高效能機器學習服務可以使用遠端計算內容，以支援的資料平台的完整範圍的解決方案。 您可以移動執行從本機伺服器至遠端的 Machine Learning Server 或另一個 SQL Server 執行個體上的 Spark 叢集。

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>預先安裝檢查清單

如果您已安裝舊的版本中，例如 SQL Server 2016 R Server （獨立式） 或 Microsoft R Server，解除安裝現有的安裝，之後才能繼續。

一般而言，我們建議您將視為獨立伺服器和資料庫引擎執行個體感知安裝做為相互專為避免資源爭用，但如果您有足夠的資源時，沒有任何禁止對兩者都安裝在相同的實體電腦。

您的電腦上只能有一部獨立伺服器： SQL Server 2017 Machine Learning Server 或 SQL Server 2016 R Server （獨立式）。 請務必在解除安裝然後再加入一個新的版本。

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>安裝修補程式需求 

SQL Server 2016 的只有：Microsoft 發現特定版本的 Microsoft VC++ 2013 Runtime 二進位檔問題，SQL Server 必須安裝這些二進位檔。 如果未安裝 VC Runtime 二進位檔的這項更新，SQL Server 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 之前，請先遵循 [SQL Server 版本資訊](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)的指示，查看您的電腦是否需要 VC Runtime 二進位檔的修補程式。  
::: moniker-end

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動安裝精靈。

2. 按一下 **安裝**索引標籤，然後選取**新的 Machine Learning Server （獨立式） 安裝**。
    
     ![安裝 Machine Learning Server 獨立式](media/2017setup-installation-page-mlsvr.png "啟動 Machine Learning Server 獨立式安裝")

3. 規則檢查完成之後，接受 SQL Server 授權條款，並選取新的安裝。

4. 在 **特徵選取**頁面上，下列選項應該已選取：

    - Microsoft Machine Learning Server （獨立式）

    - R 和 Python 兩者都預設會選取。 您可以取消選取任一語言，但我們建議您安裝至少其中一個支援的語言。

     ![選擇 R 或 Python 的功能](media/2017setup-features-page-mlsvr-rpy.png "啟動 Machine Learning Server 獨立式安裝")
    
    您應該忽略所有其他選項。 
    
    > [!NOTE]
    > 避免安裝**共用功能**如果電腦已有安裝 SQL Server 資料庫內分析的機器學習服務。 這會建立重複的程式庫。
    > 
    > 此外，SQL Server 中執行的 R 或 Python 指令碼來為未與其他 database engine 服務所使用的記憶體相衝突的 SQL Server 所管理，而獨立 machine learning 伺服器沒有這類條件約束，並可能會干擾其他資料庫作業. 最後，資料庫管理員通常會封鎖 RDP 工作階段，通常用於運算化，透過遠端存取。
    > 
    > 基於這些理由，我們通常建議您在 SQL Server Machine Learning 服務的不同電腦上安裝 Machine Learning Server （獨立式）。

5.  接受授權條款，下載並安裝基底語言散發套件。 無法使用 [接受]  按鈕時，您可以按一下 [下一步]  。 

     ![Python 授權協議](media/2017setup-python-license.png "Python 授權合約")

6.  在 [準備安裝]  頁面上，確認您的選項並按一下 [安裝]  。

安裝完成時，請參閱[SQL Server R services 的自訂報告](../r/monitor-r-services-using-custom-reports-in-management-studio.md)因任何錯誤或警告的協助，請參閱[升級及安裝常見問題集-Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動安裝精靈。

2. 在 **安裝**索引標籤上，按一下**新的 R Server （獨立式） 安裝**。
    
     ![啟動的 R Server （獨立式） 安裝程式](media/2016-setup-installation-rsvr.png "啟動的 R Server （獨立式） 安裝程式")

3. 規則檢查完成之後，接受 SQL Server 授權條款，並選取新的安裝。

4.  在 [功能選擇]  頁面上，應該已經選取下列選項：
    
    **R Server (獨立式)**  
    
    ![功能的 R Server （獨立式） 的選項](media/2016setup-rserver-features.png "功能選項的 R Server （獨立式）")
    
    您可以忽略所有其他選項。 
    
    > [!NOTE]
    > 避免安裝**共用功能**如果您執行安裝程式的電腦上其中 R Services 已安裝的 SQL Server 資料庫內分析。 這會建立重複的程式庫。
    > 
    > SQL Server 中執行的 R 指令碼來為未與其他 database engine 服務所使用的記憶體相衝突的 SQL Server 所管理，而獨立 R 伺服器沒有這類條件約束，並可能會干擾其他資料庫作業。
    > 
    > 我們通常建議您安裝 R Server （獨立式） 不同的電腦上從 SQL Server R Services （資料庫）。

5.  接受授權條款，下載並安裝基底語言散發套件。 無法使用 [接受]  按鈕時，您可以按一下 [下一步]  。 

6.  在 [準備安裝]  頁面上，確認您的選項並按一下 [安裝]  。

安裝完成時，請參閱[SQL Server R services 的自訂報告](../r/monitor-r-services-using-custom-reports-in-management-studio.md)因任何錯誤或警告的協助，請參閱[升級及安裝常見問題集-Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
::: moniker-end

## <a name="set-environment-variables"></a>設定環境變數

您應該設定 R 功能整合只**MKL_CBWR**環境變數，以[確保一致的輸出](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)從 Intel 數學核心程式庫 (MKL) 計算。

1. 在控制台中，按一下**系統及安全性** > **System** > **進階系統設定** >  **環境變數**。

2. 建立新的使用者或系統變數。 

  + 將變數名稱設定為 `MKL_CBWR`
  + 若要設定變數值 `AUTO`

3. 重新啟動伺服器。

<a name="install-path"></a>

### <a name="default-installation-folders"></a>預設安裝資料夾

R 和 Python 開發常會在同一部電腦上有多個版本。 安裝 SQL Server 安裝程式，因為基底散發會安裝在與您用於安裝的 SQL Server 版本相關聯的資料夾中。

下表列出 Microsoft 安裝程式所建立的 R 和 Python 散發套件的路徑。 為求完整性，資料表會包含 SQL Server 安裝程式，以及 Microsoft Machine Learning Server 的獨立安裝程式所產生的路徑。

|Version| 安裝方法 | 預設資料夾|
|----|----|----|
|SQL Server 2017 Machine Learning 伺服器 （獨立式） |  SQL Server 2017 安裝程式精靈 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server （獨立式） |  Windows 的獨立安裝程式 |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server 2017 Machine Learning 服務 （資料庫） |SQL Server 2017 安裝精靈中，使用 R 語言選項|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server （獨立式） |  SQL Server 2016 安裝精靈 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services （資料庫） |SQL Server 2016 安裝精靈|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>套用更新

我們建議您將最新的累積更新套用至 database engine 和機器學習服務元件。 透過安裝程式安裝累計更新。 

在連線網際網路的裝置，您可以下載自我解壓縮的可執行檔。 自動套用更新的 database engine 會提取的累計更新現有的 R 和 Python 功能。 

在中斷連線的伺服器，則需要額外的步驟。 您必須取得 database engine 的累計更新，以及機器學習服務功能的 CAB 檔案。 所有檔案必須傳送到隔離的伺服器，並以手動方式套用。

1. 啟動與基準的執行個體。 您只可以將累計更新套用到現有的安裝：

  + 從 SQL Server 2017 初版的 machine Learning 伺服器 （獨立式）
  + 從 SQL Server 2016 的最初發行版本、 SQL Server 2016 SP 1 或 SQL Server 2016 SP 2 的 R Server （獨立式）

2. 關閉任何開啟的 R 或 Python 工作階段，並停止任何仍在系統上執行的處理程序。

3. 如果您啟用以 web 節點和 web 服務部署的計算節點執行的運算化，備份**AppSettings.json**檔案做為預防措施。 套用 SQL Server 2017 CU13 或更新版本的 revises 這個檔案，所以您可能會想要保留原始版本的備份複本。

4. 按一下 網際網路連線的裝置，您的 SQL Server 版本的累積更新連結。

  + [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

5. 下載最新的累積更新。 這是可執行檔的檔案。

6. 在連線網際網路的裝置，連按兩下.exe 以執行安裝程式並逐步執行精靈以接受授權條款、 檢閱受影響的功能，以及監視進度，直到完成為止。

7. 在伺服器上沒有網際網路連線：

   + 取得 R 和 Python 的相對應的封包檔。 如需下載連結，請參閱[下載 SQL Server 資料庫內分析上的累計更新的執行個體的封包](sql-ml-cab-downloads.md)。

   + 將所有檔案、 主要可執行檔及封包檔，以離線的電腦上的資料夾。

   + 按兩下.exe 以執行安裝程式。 沒有網際網路連線，在伺服器上安裝累計更新，系統會提示您選取的.cab 檔案的位置，對 R 和 Python。

8. 後續安裝，您已啟用 web 節點和計算節點的運算化的伺服器上編輯**AppSettings.json**，新增"MMLResourcePath 」 項目，直接在 「 MMLNativePath 」 底下：

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [執行系統管理 CLI 公用程式](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch)重新啟動網站，並計算節點。 如需步驟和語法，請參閱[監視器、 啟動，並停止 web 和計算節點](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start)。

## <a name="development-tools"></a>開發工具

開發 IDE 不會安裝成在安裝程序。 如需有關如何設定開發環境的詳細資訊，請參閱 <<c0> [ 設定 R 工具](../r/set-up-a-data-science-client.md)並[設定 Python 工具](../python/setup-python-client-tools-sql.md)。

## <a name="next-steps"></a>後續步驟

R 開發人員可以開始使用一些簡單的範例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程：在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Python 開發人員可以了解如何使用 SQL Server 中的 Python，遵循這些教學課程：

+ [教學課程：在 T-SQL 中執行 Python](../tutorials/run-python-using-t-sql.md)
+ [教學課程：適用於 Python 開發人員的資料庫內分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

若要檢視機器學習服務依據真實世界案例的範例，請參閱[機器學習服務教學課程](../tutorials/machine-learning-services-tutorials.md)。
