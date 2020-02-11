---
title: 在沒有網際網路存取的情況下安裝
description: 在隔離在網路防火牆後方的電腦上安裝 SQL Server 機器學習 R 與 Python。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e966406a20df723c453a5c8083f00f2e4989d9d0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74064133"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>在沒有網際網路存取的電腦上安裝 SQL Server 機器學習 R 和 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

根據預設，安裝程式會連線到 Microsoft 下載網站以取得適用於 SQL Server 上機器學習的必要及更新元件。 如果防火牆條件約束防止安裝程式抵達這些網站，您可以使用已連線到網際網路的裝置來下載這些檔案，將檔案傳輸到離線伺服器，然後再執行安裝程式。

資料庫內分析包含資料庫引擎執行個體，以及適用於 R 和 Python 整合的其他元件 (視 SQL Server 的版本而定)。 

+ SQL Server 2019 包含 R、Python 及 Java
+ SQL Server 2017 包含 R 和 Python
+ SQL Server 2016 僅包含 R

在獨立的伺服器上，機器學習和 R/Python 語言特定功能是透過 CAB 檔案新增。 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
## <a name="sql-server-2019-offline-install"></a>SQL Server 2019 離線安裝

若要在獨立的伺服器上安裝 SQL Server 機器學習服務 (R 和 Python)，請先下載 SQL Server 的初始版本，以及支援 R 及 Python 的相對應 CAB 檔案。 即使您計畫立即更新伺服器以使用最新的累積更新，也必須先安裝初始版本。

> [!Note]
> SQL Server 2019 並沒有 Service Pack。 初始版本是唯一的基準線，並僅透過累積更新來提供服務。

### <a name="1---download-2019-cabs"></a>1 - 下載 2019 CAB

在具有網際網路連線的電腦上，下載適用於初始版本且提供 R 和 Python 功能的 CAB 檔案，以及 SQL Server 2019 的安裝媒體。

版本  |下載連結  |
---------|---------------|
Microsoft R Open        | [SRO_3.5.2.125_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085686) |
Microsoft R 伺服器      | [SRS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085792) |
Microsoft Python Open   | [SPO_4.5.12.120_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085793) |
Microsoft Python Server | [SPS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085685) |

> [!NOTE]
> Java 功能會包含在 SQL Server 安裝媒體中，且不需要個別的 CAB 檔案。

###  <a name="2---get-sql-server-2019-installation-media"></a>2 - 取得 SQL Server 2019 安裝媒體

1. 在具有網際網路連線的電腦上，下載 [SQL Server 2019 安裝程式](https://www.microsoft.com/sql-server/sql-server-downloads)。 

2. 按兩下安裝程式並選擇 [下載媒體]  安裝類型。 使用此選項時，安裝程式會建立包含安裝媒體的本機 .iso (或 .cab) 檔案。

   ![選擇下載媒體安裝類型](media/2019offline-download-tile.png "下載媒體")

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
## <a name="sql-server-2017-offline-install"></a>SQL Server 2017 離線安裝

若要在獨立的伺服器上安裝 SQL Server 機器學習服務 (R 和 Python)，請先下載 SQL Server 的初始版本，以及支援 R 及 Python 的相對應 CAB 檔案。 即使您計畫立即更新伺服器以使用最新的累積更新，也必須先安裝初始版本。

> [!Note]
> SQL Server 2017 並沒有 Service Pack。 它是第一個使用初始版本作為唯一基準線的 SQL Server 版本，並僅能透過累積更新來提供服務。 

### <a name="1---download-2017-cabs"></a>1 - 下載 2017 CAB

在具有網際網路連線的電腦上，下載適用於初始版本且提供 R 和 Python 功能的 CAB 檔案，以及 SQL Server 2017 的安裝媒體。 

版本  |下載連結  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R 伺服器      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2 - 取得 SQL Server 2017 安裝媒體

1. 在具有網際網路連線的電腦上，下載 [SQL Server 2017 安裝程式](https://www.microsoft.com/sql-server/sql-server-downloads)。 

2. 按兩下安裝程式並選擇 [下載媒體]  安裝類型。 使用此選項時，安裝程式會建立包含安裝媒體的本機 .iso (或 .cab) 檔案。

   ![選擇下載媒體安裝類型](media/offline-download-tile.png "下載媒體")

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="sql-server-2016-offline-install"></a>SQL Server 2016 離線安裝

SQL Server 2016 資料庫內分析僅限於 R，並只有兩個 CAB 檔案，個別適用於產品套件和 Microsoft 的開放原始碼 R 散發套件。 一開始請先安裝下列其中一個版本：RTM、SP 1、SP 2。 基底安裝完成後，便可以在下一個步驟中套用累積更新。

在具有網際網路連線的電腦上，下載安裝程式用來在 SQL Server 2016 上安裝資料庫內分析的 CAB 檔案。 

### <a name="1---download-2016-cabs"></a>1 - 下載 2016 CAB

版本  | Microsoft R Open | Microsoft R 伺服器 |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2 - 取得 SQL Server 2016 安裝媒體

您可以安裝 SQL Server 2016 RTM、SP 1 或 SP 2 作為目標電腦上的第一個安裝。 這些版本都可以接受累積更新。

取得包含安裝媒體之.iso 檔案的其中一個方法是透過 [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)。 登入，然後使用 [下載]  連結來尋找您想要安裝的 SQL Server 2016 版本。 下載的格式為 .iso 檔案，您可以將它複製到目標電腦以進行離線安裝。

::: moniker-end

## <a name="transfer-files"></a>傳輸檔案

將 SQL Server 安裝媒體 (.iso 或 .cab) 和資料庫內分析 CAB 檔案複製到目標電腦。 將 CAB 檔案和安裝媒體檔案置於目標電腦上的相同資料夾，例如安裝使用者的 %TEMP% 資料夾。

Python CAB 檔案需要使用 %TEMP% 資料夾。 針對 R，您可以使用 %TEMP% 或針對 CAB 路徑設定 `myrcachedirectory` 參數。

## <a name="run-setup"></a>執行安裝程式

當您在與網際網路中斷連線的電腦上執行 SQL Server 安裝程式時，安裝程式會在精靈中新增 [離線安裝]  頁面，讓您可以指定在上一個步驟中複製 CAB 檔案的位置。

1. 若要開始安裝，請按兩下 .iso 或 .cab 檔案以存取安裝媒體。 您應該會看見 **setup.exe** 檔案。

2. 以滑鼠右鍵按一下 **setup.exe**，然後以系統管理員身分執行。

3. 當設定精靈顯示開放原始碼 R 或 Python 元件的授權頁面時，請按一下 [接受]  。 接受授權條款可讓您繼續進行下一個步驟。

4. 當您進入 [離線安裝]  頁面時，在 [安裝路徑]  中，指定包含您先前所複製 CAB 檔案的資料夾。

5. 繼續遵循螢幕上的提示來完成安裝。

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>套用累積更新

我們建議您將最新的累積更新套用至資料庫引擎和機器學習元件。 累積更新是透過安裝程式進行安裝。 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
1. 從基準執行個體開始。 您只能將累積更新套用到 SQL Server 初始版本的現有安裝上。

2. 在連線到網際網路的裝置上，移至您 SQL Server 版本的累積更新清單：

   + SQL Server 2019 更新 (尚未提供適用於 2019 的更新) 
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
1. 從基準執行個體開始。 您只能將累積更新套用到 SQL Server 初始版本的現有安裝上。

2. 在連線到網際網路的裝置上，移至您 SQL Server 版本的累積更新清單：

   + [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/) \(英文\)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. 從基準執行個體開始。 您只能將累積更新套用到 SQL Server 2016 初始版本、SQL Server 2016 SP 1，或是 SQL Server 2016 SP 2 的現有安裝上。

2. 在連線到網際網路的裝置上，移至您 SQL Server 版本的累積更新清單：

   + [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/) \(英文\)
::: moniker-end

3. 選取最新的累積更新以下載可執行檔。

4. 取得 R 和 Python 的對應 CAB 檔案。 如需下載連結，請參閱[SQL Server 資料庫內分析執行個體之累積更新的 CAB 下載](sql-ml-cab-downloads.md)。

5. 將所有檔案 (可執行檔和 CAB 檔案) 傳送到離線電腦上的相同資料夾。

6. 執行安裝程式。 接受授權條款，然後在 [特徵選取] 頁面上，檢閱已套用累積更新的功能。 您應該會看到針對目前執行個體安裝的每個功能，包括機器學習功能。

   ![從功能樹狀目錄選取功能](media/cumulative-update-feature-selection.png "功能清單")

5. 繼續執行精靈，並接受 R 和 Python 散發套件的授權條款。 在安裝期間，系統會提示您選擇包含已更新 CAB 檔案的資料夾位置。

## <a name="set-environment-variables"></a>設定環境變數

僅針對 R 功能整合，您應該設定 **MKL_CBWR** 環境變數，以確保來自 Intel Math Kernel Library (MKL) 計算的輸出[會保持一致](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) \(英文\)。

1. 在 [控制台] 中，按一下 [系統及安全性]   > [系統]   > [進階系統設定]   > [環境變數]  。

2. 建立新的使用者或系統變數。 

   + 將變數名稱設定為 `MKL_CBWR`
   + 將變數值設定為 `AUTO`

此步驟需要重新啟動伺服器。 如果您即將啟用指令碼執行，則可以推遲重新啟動，直到完成所有設定工作為止。

## <a name="post-install-configuration"></a>安裝後續設定

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
在安裝結束之後，重新啟動服務並設定伺服器以啟用指令碼執行：

+ [啟用外部指令碼執行](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)

SQL Server 機器學習服務的初始離線安裝需要和線上安裝相同的設定：

+ [確認安裝](sql-machine-learning-services-windows-install.md#verify-installation)
+ [視需要進行其他設定](sql-machine-learning-services-windows-install.md#additional-configuration)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
在安裝結束之後，重新啟動服務並設定伺服器以啟用指令碼執行：

+ [啟用外部指令碼執行](sql-r-services-windows-install.md#bkmk_enableFeature)

SQL Server R Services 的初始離線安裝需要和線上安裝相同的設定：

+ [確認安裝](sql-r-services-windows-install.md#verify-installation)
+ [視需要進行其他設定](sql-r-services-windows-install.md#bkmk_FollowUp)
::: moniker-end

## <a name="next-steps"></a>後續步驟

若要檢查執行個體的安裝狀態並修正常見問題，請參閱[適用於 SQL Server 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

如需任何不熟悉訊息或記錄項目上的協助，請參閱[升級和安裝常見問題集 - 機器學習服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
