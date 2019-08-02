---
title: 使用 SQL Server 安裝程式安裝 R Server 或 Machine Learning Server (獨立式)
description: 使用 RevoScaleR、revoscalepy、MicrosoftML 和其他套件, 設定適用于 R 和 Python 開發的非實例感知獨立機器學習伺服器。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 94ca7b3646b9005e11b3ee4968cbfaaa65d42264
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715841"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>使用 SQL Server 安裝程式安裝 Machine Learning Server (獨立式) 或 R Server (獨立式)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server 安裝套裝程式含一個**共用功能**選項, 可用於安裝在 SQL Server 外部執行的非實例感知獨立機器學習伺服器。 它稱為**Machine Learning Server (獨立式)** , 並包含 R 和 Python。 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server 安裝套裝程式含一個**共用功能**選項, 可用於安裝在 SQL Server 外部執行的非實例感知獨立機器學習伺服器。 在 SQL Server 2016 中, 這項功能稱為**R Server (獨立式)** 。  
::: moniker-end

SQL Server 安裝程式所安裝的獨立伺服器在功能上相當於非 SQL 品牌版本的[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), 支援相同的使用案例和案例, 包括:

+ 遠端執行, 在相同主控台中的本機與遠端會話之間切換
+ 使用 web 節點和計算節點的運算化
+ Web 服務部署: 將 R 和 Python 腳本封裝成 web 服務的能力
+ R 和 Python 函式程式庫的完整集合

隨著獨立伺服器與 SQL Server 分離, R 和 Python 環境會使用基礎作業系統和獨立伺服器中提供的工具進行設定、保護和存取, 而不是 SQL Server。

如果您需要開發高效能的機器學習解決方案來使用遠端計算內容, 以支援資料平臺的完整範圍, 獨立伺服器是 SQL Server 的附屬元件。 您可以將執行從本機伺服器移至 Spark 叢集或另一個 SQL Server 實例上的遠端 Machine Learning Server。

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>預先安裝檢查清單

如果您已安裝舊版 (例如 SQL Server 2016 R Server (獨立式) 或 Microsoft R Server), 請先卸載現有的安裝, 然後再繼續。

一般來說, 我們建議您將獨立伺服器和資料庫引擎實例感知安裝視為互斥, 以避免資源爭用, 但如果您有足夠的資源, 就無法在相同的實體電腦。

電腦上只能有一部獨立伺服器: SQL Server Machine Learning Server (獨立式) 或 SQL Server R Server (獨立式)。 在新增新版本之前, 請務必先卸載其中一個版本。

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>安裝修補程式需求 

僅適用于 SQL Server 2016:Microsoft 發現特定版本的 Microsoft VC++ 2013 Runtime 二進位檔問題，SQL Server 必須安裝這些二進位檔。 如果未安裝 VC Runtime 二進位檔的這項更新，SQL Server 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 之前，請先遵循 [SQL Server 版本資訊](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)的指示，查看您的電腦是否需要 VC Runtime 二進位檔的修補程式。  
::: moniker-end

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動安裝精靈。

2. 按一下 [**安裝**] 索引標籤, 然後選取 [**新增 Machine Learning Server (獨立) 安裝**]。
    
     ![獨立安裝 Machine Learning Server](media/2017setup-installation-page-mlsvr.png "開始安裝 Machine Learning Server 獨立式")

3. 完成規則檢查之後, 請接受 SQL Server 授權條款, 然後選取新的安裝。

4. 在 [**特徵選取**] 頁面上, 應該已經選取下列選項:

    - Microsoft Machine Learning Server (獨立式)

    - 預設會選取 R 和 Python。 您可以取消選取任一種語言, 但我們建議您至少安裝其中一種支援的語言。

     ![選擇 R 或 Python 功能](media/2017setup-features-page-mlsvr-rpy.png "開始安裝 Machine Learning Server 獨立式")
    
    您應該忽略所有其他選項。 
    
    > [!NOTE]
    > 如果電腦已安裝 Machine Learning 服務以進行資料庫內分析 SQL Server, 請避免安裝**共用功能**。 這會建立重複的程式庫。
    > 
    > 此外, 雖然在 SQL Server 中執行的 R 或 Python 腳本是由 SQL Server 管理, 因此不會與其他 database engine 服務所使用的記憶體衝突, 獨立機器學習伺服器沒有這類條件約束, 而且可能會干擾其他資料庫作業. 最後, 透過 RDP 會話的遠端存取通常用於運算化, 通常是由資料庫管理員封鎖。
    > 
    > 基於這些理由, 我們通常建議您從 SQL Server Machine Learning 服務, 在另一部電腦上安裝 Machine Learning Server (獨立式)。

5.  接受下載和安裝基礎語言散發套件的授權條款。 無法使用 [接受] 按鈕時，您可以按一下 [下一步]。 

     ![Python 授權合約](media/2017setup-python-license.png "Python 授權合約")

6.  在 [準備安裝] 頁面上，確認您的選項並按一下 [安裝]。

安裝完成時, 請參閱[SQL Server R Services 的自訂報告](../r/monitor-r-services-using-custom-reports-in-management-studio.md), 以取得任何錯誤或警告的說明, 請參閱[升級和安裝常見問題-Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>執行安裝程式

如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。

1. 啟動安裝精靈。

2. 在 [**安裝**] 索引標籤上, 按一下 [**新增 R Server (獨立式) 安裝**]。
    
     ![啟動 R 伺服器獨立安裝](media/2016-setup-installation-rsvr.png "啟動 R 伺服器獨立安裝")

3. 完成規則檢查之後, 請接受 SQL Server 授權條款, 然後選取新的安裝。

4.  在 [功能選擇] 頁面上，應該已經選取下列選項：
    
    **R Server (獨立式)**  
    
    ![適用于 R Server 獨立的功能選取](media/2016setup-rserver-features.png "適用于 R Server 獨立的功能選取")
    
    您可以忽略所有其他選項。 
    
    > [!NOTE]
    > 如果您是在已安裝 R Services 進行 SQL Server 資料庫內分析的電腦上執行安裝程式, 請避免安裝**共用的功能**。 這會建立重複的程式庫。
    > 
    > 雖然在 SQL Server 中執行的 R 腳本是由 SQL Server 管理, 因此不會與其他 database engine 服務所使用的記憶體衝突, 獨立 R 伺服器也沒有這類條件約束, 而且可能會干擾其他資料庫作業。
    > 
    > 我們通常會建議您將 R Server (獨立式) 安裝在與 SQL Server R Services (資料庫內) 不同的電腦上。

5.  接受下載和安裝基礎語言散發套件的授權條款。 無法使用 [接受] 按鈕時，您可以按一下 [下一步]。 

6.  在 [準備安裝] 頁面上，確認您的選項並按一下 [安裝]。

安裝完成時, 請參閱[SQL Server R Services 的自訂報告](../r/monitor-r-services-using-custom-reports-in-management-studio.md), 以取得任何錯誤或警告的說明, 請參閱[升級和安裝常見問題-Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
::: moniker-end

## <a name="set-environment-variables"></a>設定環境變數

僅適用于 R 功能整合, 您應該設定**MKL_CBWR**環境變數, 以確保從 Intel 數學核心程式庫 (MKL) 計算的[輸出一致](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)。

1. 在 [控制台] 中, 按一下 [**系統及安全性** > **系統** > ] [系統**設定** > ] [**環境變數**]。

2. 建立新的使用者或系統變數。 

  + 將變數名稱設定為`MKL_CBWR`
  + 將變數值設定為`AUTO`

3. 重新啟動伺服器。

<a name="install-path"></a>

### <a name="default-installation-folders"></a>預設安裝資料夾

針對 R 和 Python 開發, 同一部電腦上通常會有多個版本。 如 SQL Server 安裝程式所安裝, 基底發佈會安裝在與您用於安裝之 SQL Server 版本關聯的資料夾中。

下表列出由 Microsoft 安裝程式所建立之 R 和 Python 散發套件的路徑。 為求完整性, 此表格包含 SQL Server 安裝程式所產生的路徑, 以及 Microsoft Machine Learning Server 的獨立安裝程式。

|Version| 安裝方法 | 預設資料夾|
|----|----|----|
|SQL Server 2017 Machine Learning Server (獨立) |  SQL Server 2017 安裝程式嚮導 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (獨立式) |  Windows 獨立安裝程式 |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server Machine Learning 服務 (資料庫內) |使用 R 語言選項 SQL Server 2017 安裝程式嚮導|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (獨立式) |  SQL Server 2016 安裝程式嚮導 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (資料庫內) |SQL Server 2016 安裝程式嚮導|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>套用更新

我們建議您將最新的累計更新套用至資料庫引擎和機器學習服務元件。 累計更新是透過安裝程式進行安裝。 

在連線到網際網路的裝置上, 您可以下載自我解壓縮的可執行檔。 為資料庫引擎套用更新時, 會自動提取現有 R 和 Python 功能的累計更新。 

在中斷連線的伺服器上, 需要額外的步驟。 您必須取得資料庫引擎的累計更新以及機器學習功能的 CAB 檔案。 所有檔案都必須傳輸到隔離伺服器, 並以手動方式套用。

1. 從基準實例開始。 您只能將累計更新套用到現有的安裝:

  + SQL Server 2017 初始版本的 Machine Learning Server (獨立式)
  + 來自 SQL Server 2016 初始版本、SQL Server 2016 SP 1 或 SQL Server 2016 SP 2 的 R Server (獨立式)

2. 關閉任何開啟的 R 或 Python 會話, 並停止任何仍在系統上執行的進程。

3. 如果您已啟用運算化作為 web 服務部署的網路節點和計算節點, 請備份**AppSettings**作為預防措施。 套用 SQL Server 2017 CU13 或更新版本會修訂此檔案, 因此您可能會想要保留原始版本的備份複本。

4. 在連線到網際網路的裝置上, 按一下您 SQL Server 版本的 [累計更新] 連結。

  + [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

5. 下載最新的累積更新。 這是可執行檔。

6. 在連線到網際網路的裝置上, 按兩下 .exe 以執行安裝程式, 並逐步執行嚮導以接受授權條款、檢查受影響的功能, 並監視進度直到完成為止。

7. 在沒有網際網路連線的伺服器上:

   + 取得 R 和 Python 的對應 CAB 檔案。 如需下載連結, 請參閱[SQL Server 資料庫內分析實例上的累積更新的 CAB 下載](sql-ml-cab-downloads.md)。

   + 將所有檔案 (主要可執行檔和 CAB 檔案) 傳送到離線電腦上的資料夾。

   + 按兩下 .exe 以執行安裝程式。 在沒有網際網路連線的伺服器上安裝累計更新時, 系統會提示您選取 R 和 Python 之 .cab 檔案的位置。

8. 安裝後, 在您已使用 web 節點和計算節點啟用運算化的伺服器上, 編輯**AppSettings**, 並在 "MMLNativePath" 正下方新增 "MMLResourcePath" 專案:

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [執行系統管理員 CLI 公用程式](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch), 以重新開機 web 和計算節點。 如需步驟和語法, 請參閱[監視、啟動和停止 web 和計算節點](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start)。

## <a name="development-tools"></a>開發工具

開發 IDE 不會安裝為安裝程式的一部分。 如需設定開發環境的詳細資訊, 請參閱安裝[R 工具](../r/set-up-a-data-science-client.md)和[設定 Python 工具](../python/setup-python-client-tools-sql.md)。

## <a name="next-steps"></a>後續步驟

R 開發人員可以開始使用一些簡單的範例, 並瞭解 R 如何與 SQL Server 搭配運作的基本概念。 如需下一個步驟, 請參閱下列連結:

+ [教學課程：在 T-sql 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教學課程：適用于 R 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Python 開發人員可以遵循下列教學課程, 瞭解如何搭配使用 Python 與 SQL Server:

+ [教學課程：在 T-sql 中執行 Python](../tutorials/run-python-using-t-sql.md)
+ [教學課程：適用于 Python 開發人員的資料庫內分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

若要查看以真實世界案例為基礎的機器學習範例, 請參閱[機器學習服務教學課程](../tutorials/machine-learning-services-tutorials.md)。
