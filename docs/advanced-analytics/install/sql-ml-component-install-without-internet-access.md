---
title: 安裝 R 語言和沒有網際網路存取-SQL Server Machine Learning 的 Python 元件
description: 離線或已中斷連線 Machine Learning R 和 Python 安裝程式在隔離網路防火牆後方的 SQL Server 執行個體上。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c14f6c3c404cee8a4197672c851cf1358b9a8d9b
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511915"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>安裝 SQL Server machine learning 無法存取網際網路的電腦上的 R 和 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

根據預設，連接到 Microsoft 下載網站取得必要的安裝程式和更新的元件，用於機器學習 SQL Server 上。 如果防火牆限制會防止安裝程式，使其無法到達這些站台，您可以使用網際網路連線的裝置，若要下載檔案，將檔案傳送到離線的伺服器，然後再執行安裝程式。

在資料庫內分析是由資料庫引擎執行個體，再加上對於 R 和 Python 的整合，根據 SQL Server 版本的其他元件所組成。 

+ SQL Server 2017 包含 R 和 Python 
+ SQL Server 2016 是僅限 R。

在獨立伺服器上，machine learning 及 R/Python 語言特有的功能會加入到封包檔。 

## <a name="sql-server-2017-offline-install"></a>SQL Server 2017 的離線安裝

若要隔離的伺服器上安裝 SQL Server 2017 Machine Learning 服務 （R 和 Python），開始下載 SQL Server 的初始版本，並相對應的封包檔，對 R 和 Python 支援。 即使您打算立即更新您的伺服器，以使用最新的累積更新時，必須先安裝的初始版本。

> [!Note]
> SQL Server 2017 沒有 service pack。 它是作為唯一的基準線，透過僅限累積更新提供服務的初始版本的 SQL Server 的第一個版本。 

### <a name="1---download-2017-cabs"></a>1-下載 2017 Cab

在具有網際網路連線的電腦，下載封包檔的初始版本和安裝媒體中提供 R 和 Python 的功能，SQL Server 2017。 

版本  |下載連結  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2-取得 SQL Server 2017 安裝媒體

1. 在具有網際網路連線的電腦，下載[SQL Server 2017 安裝程式](https://www.microsoft.com/sql-server/sql-server-downloads)。 

2. 按兩下安裝程式，並選擇**下載媒體**安裝類型。 使用此選項時，安裝程式會建立包含安裝媒體的本機.iso （或.cab） 檔案。

   ![選擇下載媒體的安裝類型](media/offline-download-tile.png "下載媒體")

## <a name="sql-server-2016-offline-install"></a>SQL Server 2016 的離線安裝

SQL Server 2016 資料庫內分析是 R 僅，搭配正是其中兩個封包檔產品套件和 Microsoft 發佈的開放原始碼 R，分別。 先安裝這些版本的任何一個：RTM, SP 1, SP 2. 就地的基底安裝之後，可以在下一個步驟套用累計更新。

在具有網際網路連線的電腦，下載安裝程式用來安裝 SQL Server 2016 上的資料庫內分析封包檔。 

### <a name="1---download-2016-cabs"></a>1-下載 2016 Cab

版本  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038) |

### <a name="2---get-sql-server-2016-installation-media"></a>2-取得 SQL Server 2016 安裝媒體

您可以為您的第一次安裝在目標電腦上安裝 SQL Server 2016 RTM、 SP 1 或 SP 2。 這些版本其中任何一個可接受的累計更新。

其中一種方式取得.iso 檔案包含安裝媒體是透過[Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)。 登入，然後再使用**下載**連結，來尋找您想要安裝的 SQL Server 2016 版本。 下載的.iso 檔案，您可以複製到目標電腦上進行離線安裝的格式。

## <a name="transfer-files"></a>非同步傳送檔案

SQL Server 安裝媒體 （.iso 或.cab） 和資料庫內分析封包檔案複製到目標電腦。 將封包檔和安裝媒體檔案放在目標電腦，例如安裝程式使用者的 %temp * 資料夾上的相同資料夾中。

Python 封包檔需要 %TEMP%資料夾。 針對 R，您可以使用 %TEMP%，或將 myrcachedirectory 參數設為封包的路徑。

下列螢幕擷取畫面顯示 SQL Server 2017 CAB 及 ISO 檔案。 SQL Server 2016 的下載項目看起來不一樣： 較少的檔案 (沒有 Python) 和安裝媒體檔案名稱是適用於 2016年。

![要傳送的檔案清單](media/offline-file-list.png "檔案清單")

## <a name="run-setup"></a>執行安裝程式

當您與網際網路中斷連線的電腦上執行 SQL Server 安裝程式時，安裝程式會新增**離線安裝**精靈 頁面上，好讓您可以指定您在上一個步驟中複製的封包檔的位置。

1. 若要開始安裝，請按兩下的.iso 或.cab 檔，以存取安裝媒體。 您應該會看到**setup.exe**檔案。

2. 以滑鼠右鍵按一下**setup.exe**系統管理員身分執行。

3. 當安裝精靈顯示的開放原始碼 R 或 Python 元件的 授權 頁面時，按一下 **接受**。 接受授權條款，可讓您繼續進行下一個步驟。

4. 當您進入**離線安裝**頁面上，於**安裝路徑**，指定包含您稍早複製的封包檔的資料夾。

   ![精靈頁面的封包資料夾選擇](media/screenshot-sql-offline-cab-page.png "封包資料夾")

5. 繼續下螢幕上的提示完成安裝。

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>套用累計更新

我們建議您將最新的累積更新套用至 database engine 和機器學習服務元件。 透過安裝程式安裝累計更新。 

1. 啟動與基準的執行個體。 您只可以將累計更新套用到現有安裝的 SQL Server:

  + SQL Server 2017 的初始版本
  + SQL Server 2016 的最初發行版本、 SQL Server 2016 SP 1 或 SQL Server 2016 SP 2

2. 在 網際網路連線的裝置，請移至您的 SQL Server 版本的累積更新清單：

  + [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

3. 選取要下載可執行檔的最新累積更新。

4. 取得 R 和 Python 的相對應的封包檔。 如需下載連結，請參閱[下載 SQL Server 資料庫內分析上的累計更新的執行個體的封包](sql-ml-cab-downloads.md)。

5. 將所有的檔案、 可執行檔及封包檔，以離線的電腦上的相同資料夾。

6. 執行安裝程式。 接受授權條款，並在 特徵選取 頁面中，檢閱 ，套用累計更新的功能。 您應該會看到安裝目前的執行個體，包括機器學習服務功能的每項功能。

  ![從功能樹狀目錄中選取的功能](media/cumulative-update-feature-selection.png "功能清單")

5. 繼續執行精靈，並接受 R 和 Python 散發套件的授權條款。 在安裝期間，系統會提示您選擇 包含更新的封包檔的資料夾位置。

## <a name="set-environment-variables"></a>設定環境變數

您應該設定 R 功能整合只**MKL_CBWR**環境變數，以[確保一致的輸出](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)從 Intel 數學核心程式庫 (MKL) 計算。

1. 在控制台中，按一下**系統及安全性** > **System** > **進階系統設定** >  **環境變數**。

2. 建立新的使用者或系統變數。 

  + 將變數名稱設定為 `MKL_CBWR`
  + 若要設定變數值 `AUTO`

此步驟需要重新啟動伺服器。 如果您要啟用指令碼執行，您可以延後重新啟動後的所有組態工作完成前。

## <a name="post-install-configuration"></a>安裝後續設定

安裝完成之後，重新啟動服務，然後設定 啟用指令碼執行的伺服器：

+ [啟用外部指令碼執行 (SQL Server 2017)](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)
+ [啟用外部指令碼執行 (SQL Server 2016)](sql-r-services-windows-install.md#bkmk_enableFeature)

SQL Server 2017 Machine Learning 服務或 SQL Server 2016 R Services 的初始離線安裝需要線上安裝相同的組態：

+ [確認安裝是否](sql-machine-learning-services-windows-install.md#verify-installation)(如 SQL Server 2016 中，按一下[這裡](sql-r-services-windows-install.md#verify-installation))。
+ [額外的設定，視](sql-machine-learning-services-windows-install.md#additional-configuration)(如 SQL Server 2016 中，按一下[這裡](sql-r-services-windows-install.md#bkmk_FollowUp))。

## <a name="next-steps"></a>後續步驟

若要檢查的執行個體的安裝狀態，並修正常見的問題，請參閱[SQL Server R services 的自訂報告](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

如需協助任何不熟悉的訊息或記錄檔項目，請參閱[升級及安裝常見問題集-Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

