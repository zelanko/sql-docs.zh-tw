---
title: 應用程式部署擴充功能
titleSuffix: SQL Server big data clusters
description: 將 Python 或 R 指令碼部署為 SQL Server 2019 巨量資料叢集 （預覽） 上的應用程式。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: jroth
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0b0d76db3813e0a399f1ece841d729711743cbd9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801911"
---
# <a name="how-to-use-vs-code-to-deploy-applications-to-sql-server-big-data-clusters"></a>如何使用 VS Code 來部署應用程式到 SQL Server 的巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何使用 Visual Studio Code 部署應用程式擴充功能的 SQL Server 巨量資料叢集來部署應用程式。 CTP 2.3 中引進了這項功能。 

## <a name="prerequisites"></a>先決條件

- [Visual Studio Code](https://code.visualstudio.com/)。
- [SQL Server 的巨量資料叢集](big-data-cluster-overview.md)CTP 2.3 或更新版本。

## <a name="capabilities"></a>Capabilities

此延伸模組會在 Visual Studio Code 支援下列工作：

- 使用巨量資料的 SQL Server 叢集進行驗證。
- 擷取支援的執行階段的部署的 GitHub 存放庫中的應用程式範本。
- 管理使用者的工作區中目前開啟的應用程式範本。
- 部署應用程式透過 YAML 格式的規格。
- 管理 SQL Server 的巨量資料叢集內的已部署應用程式。
- 檢視所有已部署的應用程式中的其他資訊的側邊列。
- 產生使用應用程式，或從叢集刪除應用程式是執行的規格。
- 使用已部署的應用程式，透過執行規格 YAML。

下列各節逐步透過安裝程序，並提供擴充功能的運作方式概觀。 

### <a name="install"></a>安裝

在 VS Code 中，第一次安裝應用程式部署延伸模組：

1. 下載[應用程式部署的擴充功能](https://aka.ms/app-deploy-vscode)一部分 VS Code 中安裝擴充功能。

1. 啟動 VS Code，並瀏覽至 擴充功能 」 資訊看板。

1. 按一下 `…`提要欄位，然後選取頂端的快顯功能表`Install from vsix`。

   ![安裝 VSIX](media/vs-extension/install_vsix.png)

1. 尋找`sqlservbdc-app-deploy.vsix`您所下載檔案，然後選擇的安裝。

SQL Server 的巨量資料叢集應用程式部署之後在安裝延伸模組，它會提示您重新載入 VS Code。 現在，您應該會看到 SQL Server BDC 應用程式總管，VS Code 資訊看板中。

### <a name="app-explorer"></a>App Explorer

按一下 載入側邊面板，以顯示 應用程式總管 中的資訊看板中的擴充功能。 [應用程式總管] 中的下列範例螢幕擷取畫面會顯示任何應用程式或可用的應用程式規格：

<img src="media/vs-extension/app_explorer.png" width=350px></img>
<!--![App Explorer](media/vs-extension/app_explorer.png)-->

#### <a name="new-connection"></a>新的連接

若要連接到叢集端點，請使用其中一種下列方法：

- 按一下下方顯示的 狀態 列上的  `SQL Server BDC Disconnected`。
- 或按一下`New Connection`以箭號指向門廊到頂端的按鈕。

   ![新的連接](media/vs-extension/connect_to_cluster.png)

VS Code 會提示輸入適當的端點、 使用者名稱和密碼。 如果指定正確的認證和應用程式端點，VS Code 會通知您已連線到叢集，您會看到資訊看板中填入任何部署的應用程式。 如果您已成功連線時，您的端點和使用者名稱將會儲存到`./sqldbc`做為您的使用者設定檔的一部分。 以往會儲存任何密碼或語彙基元。 一次登入時，提示會預先填入您的已儲存的主應用程式和使用者名稱，但一律會要求您輸入密碼。 如果您想要連接到不同的叢集端點，只要按一下`New Connection`一次。 如果您關閉 VS Code，或如果您開啟不同的工作區，而且您必須重新連線，將會自動關閉連線。

### <a name="app-template"></a>應用程式範本

若要部署新的應用程式的其中一個範本，請按一下`New App Template`按鈕`App Specifications` 窗格中，您提示的名稱、 執行階段，以及您想要在本機電腦上放置新的應用程式中的位置。 建議您，您將它放在您目前的 VS Code 工作區，讓您可以使用延伸模組的完整功能，但您可以將它任意處置於您的本機檔案系統。

![新的應用程式範本](media/vs-extension/new_app_template.png)

完成後，新的應用程式範本建立結構，在您所指定的位置和部署`spec.yaml`會在您的工作區中開啟。 如果您選擇的目錄是在您的工作區中，您應該也會看到它列在 `App Specifications`窗格：

![已載入的應用程式範本](media/vs-extension/loading_app_template.png)

範本是一項簡單`Hello World`配置，如下所示的應用程式：

- **spec.yaml**
   - 會告知叢集如何部署您的應用程式
- **run-spec.yaml**
   - 會告知叢集如何您想要呼叫您的應用程式
- **handler.py**
   - 這是您的原始程式碼檔所指定`src`中 `spec.yaml`
   - 它有一個函式，呼叫`handler`這會視為`entrypoint`應用程式中所示的`spec.yaml`。 它會採用名的字串輸入`msg`，並傳回呼叫的字串輸出`out`。 這些條件指定於`inputs`並`outputs`的`spec.yaml`。

如果您不想包含 scaffold 的範本，並不只是想`spec.yaml`針對您已建置的應用程式的部署，按一下`New Deploy Spec`按鈕旁`New App Template` 按鈕，然後移至相同的程序，但您只會收到`spec.yaml`，您可以修改您所選擇的方式。

### <a name="deploy-app"></a>部署應用程式

您可以立即部署此應用程式，透過程式碼功能濾鏡`Deploy App`中`spec.yaml`或按下 [閃電資料夾] 按鈕旁`spec.yaml`應用程式規格功能表中的檔案。 延伸模組將壓縮的目錄中的所有檔案，您`spec.yaml`位於和您的應用程式部署到叢集。 

>[!NOTE]
>請確認所有的應用程式檔案都在相同的目錄中您`spec.yaml`。 `spec.yaml`必須位於您的應用程式的原始程式碼目錄的根層級。 

![部署應用程式按鈕](media/vs-extension/deploy_app_lightning.png)

![部署應用程式 CodeLens](media/vs-extension/deploy_app_codelens.png)

當應用程式已可供使用的資訊看板中的應用程式狀態為基礎，您將會收到通知：

![部署應用程式](media/vs-extension/app_deploy.png)

![應用程式已準備好提要欄位](media/vs-extension/app_ready_side_bar.png)

![應用程式就緒通知](media/vs-extension/app_ready_notification.png)

從側邊窗格中，您將能夠看到您可用下列：

您可以檢視所有已部署的應用程式在側邊列中，以下列資訊：

- state
- version
- 輸入參數
- 輸出參數
- 連結
  - swagger
  - 詳細資料

如果您按一下`Links`，您會看到您可以存取`swagger.json`已部署的應用程式，讓您可以撰寫您自己的用戶端會呼叫您的應用程式：

![swagger](media/vs-extension/swagger.png)

請參閱[巨量資料叢集上的應用程式會耗用](big-data-cluster-consume-apps.md)如需詳細資訊。

### <a name="app-run"></a>應用程式執行

應用程式準備就緒後，呼叫應用程式與`run-spec.yaml`所指定的應用程式範本的一部分：

![執行規格](media/vs-extension/run_spec.png)

指定您想要的位置的任何字串`hello`，然後再次執行它透過程式碼功能濾鏡連結或提要欄位中的 [閃電] 按鈕旁`run-spec.yaml`。 如果您因為任何原因沒有執行規格，請在叢集中產生一個從已部署的應用程式：

![取得執行規格](media/vs-extension/get_run_spec.png)

一旦您有一個，並已編輯您的滿意度，執行它。 應用程式完成執行時，VS Code 會傳回適當的回應：

![應用程式輸出](media/vs-extension/app_output.png)

如您從上面所見，輸出指定在暫時`.json`工作區中的檔案。 如果您想要保留此輸出，請放心將它儲存，否則它將會刪除在結尾。 如果您的應用程式不有任何輸出列印到檔案，則只會收到`Successful App Run`底部的通知。 如果您沒有執行成功，您會收到適當的錯誤訊息，可協助您判斷錯誤原因。

當執行應用程式時，有各種不同的方式來將參數傳遞：

您可以指定透過所需的所有輸入`.json`，也就是：

- `inputs: ./example.json`

當呼叫已部署的應用程式中，如果任何輸入的參數是對中炫耀應用程式或指定的使用者，而且，給定的輸入參數不是基本類型，例如陣列、 向量、 資料框架，複雜 JSON 等指定參數型別直接企業時也就呼叫應用程式中：

- 向量
    - `inputs:`
        - `x: [1, 2, 3]`
- 矩陣
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Object
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

或提供字串做為相對或絕對檔案路徑`.txt`， `.json`，或`.csv`的應用程式需要的格式提供必要的輸入。 檔案剖析為基礎`Node.js Path library`，其中的檔案路徑定義為`string that contains a / or \ character`。

如果未提供輸入的參數，視需要適當的錯誤訊息會顯示不正確的檔案路徑，如果已指定字串的檔案路徑，或該參數無效。 責任交給應用程式的建立者，以確保他們了解他們正在定義的參數。

若要刪除應用程式，只要按一下 資源回收筒可以旁邊的按鈕中的應用程式`Deployed Apps`側邊窗格。

## <a name="next-steps"></a>後續步驟

探索如何整合在您的應用程式中的巨量資料叢集的 SQL Server 上部署的應用程式[巨量資料叢集上的應用程式會耗用](big-data-cluster-consume-apps.md)如需詳細資訊。 您也可以參考其他樣本[應用程式部署範例](https://aka.ms/sql-app-deploy)嘗試擴充功能。

如需有關 SQL Server 的巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。


我們的目標是為了讓此延伸模組有助於您和我們歡迎您提供意見反應。 請傳送到[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]小組](https://aka.ms/sqlfeedback)。
