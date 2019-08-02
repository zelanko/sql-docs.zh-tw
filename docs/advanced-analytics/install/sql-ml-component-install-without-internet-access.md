---
title: 在沒有網際網路存取的情況下安裝 R 語言和 Python 元件
description: 在網路防火牆後方隔離的 SQL Server 實例上, Machine Learning R 和 Python 安裝程式離線或中斷連線。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ddeea99addae3229575ca581f344332587e85981
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715819"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>在沒有網際網路存取的電腦上安裝 SQL Server machine learning R 和 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

根據預設, 安裝程式會連線到 Microsoft 下載網站, 以取得 SQL Server 上機器學習服務的必要和更新元件。 如果防火牆條件約束阻止安裝程式到達這些網站, 您可以使用連接網際網路的裝置來下載檔案、將檔案傳輸到離線服務器, 然後執行安裝程式。

資料庫內分析包含 database engine 實例, 以及 R 和 Python 整合的其他元件, 視 SQL Server 版本而定。 

+ SQL Server 2017 和更新版本包含 R 和 Python 
+ SQL Server 2016 僅限 R。

在隔離的伺服器上, 機器學習服務和 R/Python 語言特有的功能會透過 CAB 檔案新增。 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="sql-server-2017-offline-install"></a>SQL Server 2017 離線安裝

若要在隔離的伺服器上安裝 SQL Server Machine Learning Services (R 和 Python), 請先下載 SQL Server 的初始版本, 以及 R 和 Python 支援的對應 CAB 檔案。 即使您打算立即補救伺服器以使用最新的累積更新, 還是必須先安裝初始版本。

> [!Note]
> SQL Server 2017 沒有 service pack。 第一版的 SQL Server 是使用初始版本做為唯一的基礎行, 只透過累計更新提供服務。 

### <a name="1---download-2017-cabs"></a>1-下載 2017 Cab

在具有網際網路連線的電腦上, 下載提供 R 和 Python 功能以供初始版本和 SQL Server 2017 安裝媒體的 CAB 檔案。 

版本  |下載連結  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python 開啟     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2-取得 SQL Server 2017 安裝媒體

1. 在具有網際網路連線的電腦上, 下載[SQL Server 2017 安裝程式](https://www.microsoft.com/sql-server/sql-server-downloads)。 

2. 按兩下 [安裝], 然後選擇 [**下載媒體**] 安裝類型。 使用此選項時, 安裝程式會建立包含安裝媒體的本機 .iso (或 .cab) 檔案。

   ![選擇 [下載媒體] 安裝類型](media/offline-download-tile.png "下載媒體")

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="sql-server-2016-offline-install"></a>SQL Server 2016 離線安裝

SQL Server 2016 資料庫內分析僅限 R, 其中只有兩個適用于產品套件的 CAB 檔案和 Microsoft 的開放原始碼 R 散發。 一開始請先安裝下列其中一個版本:RTM, SP 1, SP 2。 基本安裝完成後, 就可以在下一個步驟中套用累計更新。

在具有網際網路連線的電腦上, 下載安裝程式所使用的 CAB 檔案, 以在 SQL Server 2016 上安裝資料庫內分析。 

### <a name="1---download-2016-cabs"></a>1-下載 2016 Cab

版本  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2-取得 SQL Server 2016 安裝媒體

您可以安裝 SQL Server 2016 RTM、SP 1 或 SP 2, 做為您在目的電腦上的第一次安裝。 其中任何一種版本都可以接受累計更新。

取得包含安裝媒體之 .iso 檔案的其中一種方式是透過[Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)。 登入, 然後使用 [**下載**] 連結來尋找您想要安裝的 SQL Server 2016 版本。 下載的格式為 .iso 檔案, 您可以將其複製到目的電腦進行離線安裝。

::: moniker-end

## <a name="transfer-files"></a>傳輸檔案

將 SQL Server 安裝媒體 (.iso 或 .cab) 和資料庫內分析 CAB 檔案複製到目的電腦。 將 CAB 檔案和安裝媒體檔案放在目的電腦上的相同資料夾中, 例如安裝使用者的% TEMP * 資料夾。

Python CAB 檔案需要% TEMP% 資料夾。 針對 R, 您可以使用% TEMP%, 或將 myrcachedirectory 參數設定為 CAB 路徑。

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
下列螢幕擷取畫面顯示 SQL Server CAB 和 ISO 檔案。 

![要傳送的檔案清單]檔案(media/offline-file-list.png "清單")
::: moniker-end

## <a name="run-setup"></a>執行安裝程式

當您在與網際網路中斷連線的電腦上執行 SQL Server 安裝程式時, 安裝程式會將**離線安裝**頁面新增至嚮導, 讓您可以指定您在上一個步驟中複製之 CAB 檔案的位置。

1. 若要開始安裝, 請按兩下 .iso 或 .cab 檔案以存取安裝媒體。 您應該會看到**setup.exe**檔案。

2. 在**setup.exe**上按一下滑鼠右鍵, 然後以系統管理員身分執行。

3. 當安裝程式顯示 [開放原始碼 R 或 Python 元件] 的 [授權] 頁面時, 按一下 [**接受**]。 接受授權條款可讓您繼續進行下一個步驟。

4. 當您進入**離線安裝**頁面時, 請在 [**安裝路徑**] 中, 指定包含您稍早複製之 CAB 檔案的資料夾。

   ![Cab 資料夾選取範圍的 Wizard 頁面](media/screenshot-sql-offline-cab-page.png "CAB 資料夾")

5. 繼續遵循螢幕上的提示來完成安裝。

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>套用累計更新

我們建議您將最新的累計更新套用至資料庫引擎和機器學習服務元件。 累計更新是透過安裝程式進行安裝。 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
1. 從基準實例開始。 您只能將累計更新套用至 SQL Server 初始版本的現有安裝。

2. 在連線到網際網路的裝置上, 移至您的 SQL Server 版本的累計更新清單:

  + [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. 從基準實例開始。 您只能將累計更新套用到 SQL Server 2016 初始版本、SQL Server 2016 SP 1 或 SQL Server 2016 SP 2 的現有安裝。

2. 在連線到網際網路的裝置上, 移至您的 SQL Server 版本的累計更新清單:

  + [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)
::: moniker-end

3. 選取最新的累計更新以下載可執行檔。

4. 取得 R 和 Python 的對應 CAB 檔案。 如需下載連結, 請參閱[SQL Server 資料庫內分析實例上的累積更新的 CAB 下載](sql-ml-cab-downloads.md)。

5. 將所有檔案、可執行檔和 CAB 檔案傳送到離線電腦上的相同資料夾。

6. 執行安裝程式。 接受授權條款, 然後在 [特徵選取] 頁面上, 檢查已套用累積更新的功能。 您應該會看到針對目前實例安裝的每項功能, 包括機器學習功能。

    ![從功能樹狀結構選取功能](media/cumulative-update-feature-selection.png "功能清單")

5. 繼續執行嚮導, 並接受 R 和 Python 散發套件的授權條款。 在安裝期間, 系統會提示您選擇包含已更新之 CAB 檔案的資料夾位置。

## <a name="set-environment-variables"></a>設定環境變數

僅適用于 R 功能整合, 您應該設定**MKL_CBWR**環境變數, 以確保從 Intel 數學核心程式庫 (MKL) 計算的[輸出一致](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)。

1. 在 [控制台] 中, 按一下 [**系統及安全性** > **系統** > ] [系統**設定** > ] [**環境變數**]。

2. 建立新的使用者或系統變數。 

  + 將變數名稱設定為`MKL_CBWR`
  + 將變數值設定為`AUTO`

此步驟需要重新開機伺服器。 如果您即將啟用腳本執行, 您可以在重新開機前保留, 直到完成所有設定工作為止。

## <a name="post-install-configuration"></a>安裝後續設定

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
安裝完成之後, 請重新開機服務, 然後將伺服器設定為啟用腳本執行:

+ [啟用外部腳本執行](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)

SQL Server Machine Learning 服務的初始離線安裝需要與線上安裝相同的設定:

+ [確認安裝](sql-machine-learning-services-windows-install.md#verify-installation)
+ [視需要進行其他設定](sql-machine-learning-services-windows-install.md#additional-configuration)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
安裝完成之後, 請重新開機服務, 然後將伺服器設定為啟用腳本執行:

+ [啟用外部腳本執行](sql-r-services-windows-install.md#bkmk_enableFeature)

SQL Server R Services 的初始離線安裝需要與線上安裝相同的設定:

+ [確認安裝](sql-r-services-windows-install.md#verify-installation)
+ [視需要進行其他設定](sql-r-services-windows-install.md#bkmk_FollowUp)
::: moniker-end

## <a name="next-steps"></a>後續步驟

若要檢查實例的安裝狀態, 並修正常見的問題, 請參閱[SQL Server 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

如需任何不熟悉的訊息或記錄專案的說明, 請參閱[升級和安裝常見問題-Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
