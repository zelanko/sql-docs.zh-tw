---
title: Azure 資料 Studio SQL Server 2019 擴充功能 （預覽） |Microsoft Docs
description: Azure Data Studio 的 SQL Server 2019 Preview 延伸模組
ms.custom: tools|sos
ms.date: 10/11/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.prod_service: sql-tools
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d73f4a0d55cbe3fe3bacc0b2bb68f191046fe01b
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2018
ms.locfileid: "49168785"
---
# <a name="sql-server-2019-extension-preview"></a>SQL Server 2019 擴充功能 （預覽）

SQL Server 2019 擴充功能 （預覽） 提供的預覽支援的新功能和工具支援的出貨[!INCLUDE [sql-server-2019](..\includes\sssqlv15-md.md)]。 這包括提供的預覽支援[SQL Server 2019 巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)，整合[notebook 體驗](../big-data-cluster/notebooks-guidance.md)，PolyBase [Create External Table 精靈](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json)，以及[Azure 資源總管](azure-resource-explorer.md)。

## <a name="install-the-sql-server-2019-extension-preview"></a>安裝 SQL Server 2019 擴充功能 （預覽）

若要安裝 SQL Server 2019 擴充功能 （預覽版），下載並安裝相關聯的.vsix 檔案。

1. 將 SQL Server 2019 擴充功能 （預覽版）.vsix 檔案下載到本機目錄：

   |平台|下載|發行日期|
   |:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2024911)|2018 年 9 月 24日日|
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2024587)|2018 年 9 月 24日日 |
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2024841)|2018 年 9 月 24日日 |

1. 在 Azure Data Studio 選擇**VSIX 套件安裝延伸模組**從**檔案**功能表，然後選取已下載的.vsix 檔案。

1. 選擇**是**時提示您確認安裝，並等候安裝成功的通知。

1. 選取**重新載入**以啟用該擴充功能 (只有第一次安裝擴充功能時需要)。

1. 重新載入後，擴充功能會安裝相依性。 您可以看到在 [輸出] 視窗中，進度，並可能需要幾分鐘的時間。

##  <a name="sql-server-2019-big-data-cluster-support"></a>SQL Server 2019 巨量資料叢集支援

* 按一下 **加入連接**中*物件總管*，然後選擇 **巨量資料的 SQL Server 叢集**作為連線類型。

   > [!TIP]
   > 如果您看不見**巨量資料的 SQL Server 叢集**連接類型，重新啟動 Azure Data Studio。

* 輸入主機名稱或 IP 位址的叢集端點加上使用者名稱和密碼用來連接。
* （選擇性） 包含中的易記顯示名稱**名稱**欄位。
* 按一下 [ **Connect** ，然後您可以啟動一般工作的儀表板中，瀏覽**HDFS**在物件總管] 中，並從該處執行的內容中工作。
* 若要提交 Spark 作業，針對叢集，以滑鼠右鍵按一下伺服器節點中*物件總管*，然後選擇 **提交 Spark 作業**來顯示 提交 對話方塊。
* 若要開啟 Notebook 時，請參閱下一節。

如需詳細資訊，請參閱 <<c0> [ 巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)。


## <a name="azure-data-studio-notebooks"></a>Azure Data Studio Notebook

* 其中一種以下列方式開啟 notebook:
  * 開啟新的 notebook，從*命令選擇區*。
  * 開啟 SQL Server 2019 巨量資料叢集以及其中一個的 HDFS 物件總管 樹狀結構：
    * 以滑鼠右鍵按一下伺服器節點，然後選擇**新的 Jupyter Notebook**。
    * CSV 檔案中，以滑鼠右鍵按一下，然後選擇**Notebook 中的分析**。
  * 開啟現有.ipynb 檔案從**檔案** 功能表或檔案總管 *（.ipynb 檔案必須升級為 4 或更新版本，才能正確地載入的版本）*
* 選擇 [核心]。 對於本機 notebook 執行中，選擇 [Python 3]。 針對遠端執行，選擇 PySpark 或 Spark |Scala。
* 選擇 連線到遠端執行的 SQL Server 巨量資料叢集端點 （這是不必要的本機開發與 Python 3）。
* 在 notebook 標頭加入透過按鈕的程式碼或 markdown 資料格。 移除資源回收筒可以圖示，左邊的每個資料格的資料格。
* [播放] 按鈕的程式碼儲存格，以執行資料格和切換 markdown 編輯和預覽的眼睛圖示


## <a name="azure-resource-explorer"></a>Azure 資源總管

* 若要登入 Azure，請按一下左下角的 Azure Data Studio 中的 人員 圖示並遵循對話方塊以登入 Azure。
* 登入之後，按一下三角形的 Azure 圖示的左側列 Studio 的 Azure 資料，然後展開以顯示與您訂用帳戶相關聯的 SQL 資源樹狀目錄。
* 以滑鼠右鍵按一下，或按一下任何 SQL database 或 SQL Server，以開啟 連接 對話方塊上的插頭圖示。 輸入您的密碼來連線，並將資源新增至 Azure Data Studio 物件總管。

如需詳細資訊，請參閱 < [Azure 資源總管](azure-resource-explorer.md)。


## <a name="polybase-create-external-table-wizard"></a>Polybase 建立外部資料表精靈

* 從 SQL Server 2019 的執行個體*建立外部資料表精靈*可以開啟下列三種方法：
  * 以滑鼠右鍵按一下 在伺服器上，選擇**管理**，按一下索引標籤上的 SQL Server 2019 （預覽），然後選擇**Create External Table**。
  * 與 SQL Server 2019 執行個體中選取*物件總管*，啟動*建立外部精靈*透過*命令選擇區*。
  * 中的 SQL Server 2019 資料庫上按一下滑鼠右鍵*物件總管*，然後選擇**Create External Table**。
* 在這個版本的延伸模組，您可以建立外部資料表來存取遠端 SQL Server 和 Oracle 資料表。

  > [!NOTE]
  > SQL 2019 功能的外部資料表功能時，遠端 SQL Server 可能會執行舊版的 SQL Server。

* 選擇是否要在精靈的第一頁上存取 SQL Server 或 Oracle，並繼續。
* 系統會提示您建立資料庫主要金鑰，如果其中一個不已建立 （沒有足夠的複雜性的密碼將會封鎖）。
* 建立資料來源連接，和名為遠端伺服器的認證。
* 選擇要將對應至新的外部資料表物件。
* 選擇**產生指令碼**或是**建立**以完成精靈。
* 建立外部資料表之後, 就會立即顯示在物件樹狀目錄中資料庫的建立位置。


## <a name="known-issues"></a>已知問題

* 如果建立的連接時，不會儲存密碼，例如將提交 Spark 作業的某些動作可能會失敗。
* 現有.ipynb notebook 必須升級為 4 或更新版本，才能載入內容檢視器中的版本。
