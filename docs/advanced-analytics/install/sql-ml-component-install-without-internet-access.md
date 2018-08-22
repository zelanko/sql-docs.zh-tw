---
title: 安裝 SQL Server machine learning 沒有網際網路存取的 R 和 Python 元件 |Microsoft Docs
description: 離線或已中斷連線 Machine Learning R 和 Python 安裝獨立的 SQL Server 執行個體。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 94aa87c0ecad8be94498bf5571e6e4b7ed7e1af9
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/22/2018
ms.locfileid: "40437648"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>安裝 SQL Server machine learning 無法存取網際網路的電腦上的 R 和 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

根據預設，連接到 Microsoft 下載網站取得必要的安裝程式和更新的元件，用於機器學習 SQL Server 上。 如果防火牆限制會防止安裝程式，使其無法到達這些站台，您可以使用網際網路連線的裝置，若要下載檔案，將檔案傳送到離線的伺服器，然後再執行安裝程式。

在資料庫內分析是由資料庫引擎執行個體，再加上對於 R 和 Python 的整合，根據 SQL Server 版本的其他元件所組成。 

+ SQL Server 2017 包含 R 和 Python。 
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
Microsoft Python 開放     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python 伺服器    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2-取得 SQL Server 2017 安裝媒體

1. 在具有網際網路連線的電腦，下載[SQL Server 2017 安裝程式](https://www.microsoft.com/sql-server/sql-server-downloads)。 

2. 按兩下安裝程式，並選擇**下載媒體**安裝類型。 使用此選項時，安裝程式會建立包含安裝媒體的本機.iso （或.cab） 檔案。

   ![選擇下載媒體的安裝類型](media/offline-download-tile.png "下載媒體")

## <a name="sql-server-2016-offline-install"></a>SQL Server 2016 的離線安裝

SQL Server 2016 資料庫內分析是 R 僅，搭配正是其中兩個封包檔產品套件和 Microsoft 發佈的開放原始碼 R，分別。 先安裝這些版本的任何一個： SP 2，SP 1 RTM。 就地的基底安裝之後，可以在下一個步驟套用累計更新。

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

SQL Server 安裝媒體 （.iso 或.cab） 和資料庫內分析封包檔案複製到目標電腦。 例如將封包檔和安裝媒體檔案放在目標電腦上的相同資料夾中**下載**或安裝程式使用者的 %temp * 資料夾。

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

## <a name="post-install-configuration"></a>後續安裝組態

安裝完成之後，重新啟動服務，然後設定 啟用指令碼執行的伺服器：

+ [啟用外部指令碼執行 (SQL Server 2017)](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)
+ [啟用外部指令碼執行 (SQL Server 2016)](sql-r-services-windows-install.md#bkmk_enableFeature)

SQL Server 2017 Machine Learning 服務或 SQL Server 2016 R Services 的初始離線安裝需要線上安裝相同的組態：

+ [確認安裝是否](sql-machine-learning-services-windows-install.md#verify-installation)(如 SQL Server 2016 中，按一下[這裡](sql-r-services-windows-install.md#verify-installation))。
+ [額外的設定，視](sql-machine-learning-services-windows-install.md#additional-configuration)(如 SQL Server 2016 中，按一下[這裡](sql-r-services-windows-install.md#bkmk_FollowUp))。

<a name="slipstream-upgrades"></a>

## <a name="slipstream-upgrades"></a>匯集升級

匯集安裝程式是指將補充程式或更新套用至失敗的執行個體安裝，以修正現有問題的功能。 這個方法的優點是在您執行安裝程式的同時更新 SQL Server，以避免稍後分別重新啟動。

當伺服器沒有網際網路存取時，套用服務更新，以下載更新的 SQL Server 安裝程式和對應的語言特有的封包檔的版本。 

1. 啟動與基準的執行個體。 匯集升級支援的這些版本的 SQL Server:

  + SQL Server 2017 的初始版本
  + SQL Server 2016 的初始版本
  + SQL Server 2016 SP 1
  + SQL Server 2016 SP 2

2. 取得指定的累積更新的更新的版本的 SQL Server 安裝程式。 機器學習 （R 和 Python） 功能的任何更新是以串聯的基礎資料庫引擎執行個體的累計更新。

  + [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)
  + [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)

3. 取得 R 和 Python 的相對應的封包檔。 如需下載連結，請參閱[下載 SQL Server 資料庫內分析上的累計更新的執行個體的封包](sql-ml-cab-downloads.md)。

4. 將所有檔案都放在相同的資料夾中，執行安裝程式。 在安裝期間，系統會提示您選擇的更新版的 CAB 檔案的資料夾位置。

## <a name="next-steps"></a>後續步驟

若要檢查的執行個體的安裝狀態，並修正常見的問題，請參閱[SQL Server R services 的自訂報告](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

如需協助任何不熟悉的訊息或記錄檔項目，請參閱[升級及安裝常見問題集-Machine Learning 服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

