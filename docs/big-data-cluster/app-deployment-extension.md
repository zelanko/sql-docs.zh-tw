---
title: 應用程式部署擴充功能
titleSuffix: SQL Server big data clusters
description: 在 (預覽) 上[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]將 Python 或 R 腳本部署為應用程式。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 49a59650c406e3b48394da45ad0eeb4589fc4374
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653537"
---
# <a name="how-to-use-visual-studio-code-to-deploy-applications-to-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>如何使用 Visual Studio Code 將應用程式部署至[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何使用 Microsoft Visual Studio 程式碼搭配應用程式部署擴充功能, 將應用程式部署到 SQL Server big data 叢集。 此功能是在 CTP 2.3 中引進。 

## <a name="prerequisites"></a>必要條件

- [Visual Studio Code](https://code.visualstudio.com/)
- [SQL Server big data cluster](big-data-cluster-overview.md)CTP 2.3 或更新版本

## <a name="capabilities"></a>Capabilities

此擴充功能支援在 Visual Studio Code 中執行下列工作：

- 搭配 SQL Server 巨量資料叢集進行驗證。
- 從 GitHub 存放庫擷取應用程式範本以部署支援的執行階段。
- 管理使用者工作區中目前開啟的應用程式範本。
- 透過 YAML 格式的規格部署應用程式。
- 管理 SQL Server 巨量資料叢集內的已部署應用程式。
- 在提要欄位中檢視您已部署的所有應用程式及額外資訊。
- 產生執行規格以取用應用程式，或是從叢集刪除該應用程式。
- 透過執行規格 YAML 來取用已部署應用程式。

下列各節會逐步說明安裝程序，並提供此擴充功能運作方式的概觀。 

### <a name="install"></a>安裝

請先在 Visual Studio Code 中安裝應用程式部署擴充功能:

1. 下載[應用程式部署擴充](https://aka.ms/app-deploy-vscode)功能, 以在 Visual Studio Code 中安裝延伸模組。

1. 啟動 Visual Studio Code, 然後流覽至 [擴充功能] 提要欄位。

1. 按一下提要欄位頂端的 `…` 內容功能表，然後選取 `Install from vsix`。

   ![安裝 VSIX](media/vs-extension/install_vsix.png)

1. 找到您所下載的 `sqlservbdc-app-deploy.vsix` 檔案，然後選擇它以安裝。

安裝 SQL Server big data cluster 應用程式部署擴充功能之後, 它會提示您重載 Visual Studio Code。 您現在應該會在 [Visual Studio Code] 提要欄位中看到 SQL Server BDC 應用程式瀏覽器。

### <a name="app-explorer"></a>應用程式總管

在提要欄位中按一下該擴充功能，以載入顯示 [應用程式總管] 的側邊面板。 下列的 [應用程式總管] 範例螢幕擷取畫面沒有顯示任何應用程式或應用程式規格：

![應用程式總管](media/vs-extension/app_explorer.png)

#### <a name="connect-to-cluster"></a>連接到叢集

若要連線至叢集端點，請使用下列其中一種方法：

- 按一下位於底部且顯示為 `SQL Server BDC Disconnected`的狀態列。
- 或是按一下位於頂端且具有指向門內箭號的 `Connect to Cluster` 按鈕。

Visual Studio Code 會提示您輸入適當的端點、使用者名稱和密碼。

要連接的端點是埠`Cluster Management Service` 30080 的端點。

您也可以從命令列中找到此端點。 

```
azdata bdc endpoint list
```

取得此資訊的另一種方式, 就是在伺服器上以滑鼠右鍵按一下 [**管理**], Azure Data Studio 您會在其中找到所列出服務的端點。

![廣告結束點](media/vs-extension/ads_end_point.png)

一旦找到要使用的端點, 然後連線到叢集。

![新增連線](media/vs-extension/connect_to_cluster.png)

 如果指定了正確的認證和應用程式端點, Visual Studio Code 會通知您已連線到叢集, 而且您會看到在提要欄位中填入任何已部署的應用程式。 如果您成功連線，您的端點和使用者名稱將會作為您使用者設定檔的一部分被儲存到 `./sqldbc`。 系統一律不會儲存密碼或權杖。 再次登入時，系統提示將會預先填入您已儲存的主機和使用者名稱，但一律會要求您輸入密碼。 如果您想要連線到不同的叢集端點，請再次按一下 `New Connection`。 如果您關閉 Visual Studio Code 或開啟不同的工作區, 而且需要重新連接, 連線將會自動關閉。

### <a name="app-template"></a>應用程式範本

您必須在要儲存應用程式構件的 Visual Studio Code 中*開啟工作區*。

若要利用我們的其中一個範本來部署新的應用程式，請按一下 `App Specifications` 窗格上的 `New App Template` 按鈕；系統將會提示您輸入名稱、執行階段，以及您想要在本機電腦上放置新應用程式的位置。 您提供的名稱和版本應為 DNS-1035 標籤, 且必須包含小寫英數位元或 '-'、以字母字元開頭, 並以英數位元字元結尾。

建議您將它放在目前的 Visual Studio Code 工作區, 讓您可以使用延伸模組的完整功能, 但您可以將它放在本機檔案系統的任何位置。

![新增應用程式範本](media/vs-extension/new_app_template.png)

完成後，系統會在您所指定的位置對新的應用程式範本進行 Scaffold，且 `spec.yaml` 部署會在您的工作區中開啟。 如果您所選取的目錄是位於您的工作區中，您也應該確定它已列於 `App Specifications` 窗格底下：

![已載入應用程式範本](media/vs-extension/loading_app_template.png)

範本是一個簡單`helloworld`的應用程式, 在 [應用程式規格] 窗格中配置如下:

- **spec.yaml**
   - 告訴叢集部署您應用程式的方式
- **run-spec.yaml**
   - 告訴叢集您想要呼叫應用程式的方式

應用程式的原始程式碼會在工作區資料夾中。

- **來原始檔案名**
   - 這是您的原始程式碼檔案，如 `spec.yaml` 中的 `src` 所指定
   - 它具有稱為 `handler` 的單一函式，其會被視為應用程式的 `entrypoint`，如 `spec.yaml` 中所示。 它會接受名為 `msg` 的字串輸入，並會傳回名為 `out` 的字串輸出。 這些是在 `spec.yaml` 的 `inputs` 和 `outputs` 中指定。

如果您不想要已進行 Scaffold 的範本，且只想要 `spec.yaml` 來部署您已建置的應用程式，請按一下 `New App Template` 按鈕旁邊的 `New Deploy Spec` 按鈕，然後完成相同的程序；在此情況下，您只會接收到 `spec.yaml`，其可供您視需要修改。

### <a name="deploy-app"></a>部署應用程式

您可以透過 `spec.yaml` 中的 CodeLens `Deploy App`，或是按下 [應用程式規格] 功能表中位於 `spec.yaml` 檔案旁邊的閃電資料夾按鈕，來立即部署此應用程式。 擴充功能會將 `spec.yaml` 所在目錄中的所有檔案壓縮，並將應用程式部署到叢集。 

>[!NOTE]
>請確定所有的應用程式檔案都位於和 `spec.yaml` 相同的目錄中。 `spec.yaml` 必須位於您應用程式原始程式碼目錄的根層級。 

![[部署應用程式] 按鈕](media/vs-extension/deploy_app_lightning.png)

![[部署應用程式] CodeLens](media/vs-extension/deploy_app_codelens.png)

系統會透過提要欄位中的應用程式狀態來通知您應用程式已可供使用：

![應用程式已部署](media/vs-extension/app_deploy.png)

![應用程式 [就緒] 提要欄位](media/vs-extension/app_ready_side_bar.png)

![[應用程式就緒] 通知](media/vs-extension/app_ready_notification.png)

從提要欄位，您將能看見可供您使用的下列項目：

您可以在側邊列中檢視您已部署的所有應用程式及下列資訊：

- state
- 版本
- 輸入參數
- 輸出參數
- 連結
  - Swagger
  - details

如果您按一下`Links`, 您會看到您可以`swagger.json`存取已部署應用程式的, 讓您可以撰寫自己的用戶端來呼叫您的應用程式:

![Swagger](media/vs-extension/swagger.png)

請參閱[取用巨量資料叢集上的應用程式](big-data-cluster-consume-apps.md)以取得詳細資訊。

### <a name="app-run"></a>應用程式執行

應用程式就緒之後，請使用應用程式範本隨附的 `run-spec.yaml` 來呼叫應用程式：

![執行規格](media/vs-extension/run_spec.png)

指定您想要用來取代 `hello` 的任何字串，然後再次透過 CodeLens 連結，或是提要欄位中位於 `run-spec.yaml` 旁邊的閃電按鈕來執行它。 如果您基於任何原因而沒有執行規格，請從叢集中的已部署應用程式產生一個：

![取得執行規格](media/vs-extension/get_run_spec.png)

在您取得執行規格並依照您的需求編輯它之後，請執行它。 當應用程式完成執行時, Visual Studio Code 會傳回適當的意見反應:

![應用程式輸出](media/vs-extension/app_output.png)

如您在上方所見，系統會在您工作區中以臨時 `.json` 檔案的形式提供輸出。 如果您想要保留此輸出，請儲存它；否則，系統會在 VS Code 關閉時將它刪除。 如果您的應用程式沒有可列印到檔案的輸出，您只會在底部收到 `Successful App Run` 通知。 如果您沒有成功執行，您將會收到適當的錯誤訊息，其可協助您判斷錯誤的原因。

執行應用程式時，有數種方式可以用來傳遞參數：

您可以透過 `.json` 指定所有必要的輸入，如下所示：

- `inputs: ./example.json`

呼叫已部署的應用程式時，如果有任何輸入參數是所指定應用程式或使用者已經具有的，且該指定輸入參數是基本類型以外的任何類型 (例如陣列、向量、dataframe、複雜 JSON 等)，請在呼叫應用程式時直接在行中指定該參數類型，如下所示：

- 向量
    - `inputs:`
        - `x: [1, 2, 3]`
- 矩陣
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Object
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

或是以能透過您應用程式所需的格式提供必要輸入的 `.txt`、`.json` 或 `.csv`之相對或絕對檔案路徑的形式提供字串。 檔案剖析是以 `Node.js Path library` 為基礎，其中檔案路徑會被定義為 `string that contains a / or \ character`。

如果輸入參數沒有依需求提供，系統將會搭配錯誤的檔案路徑 (如果有提供字串檔案路徑的話) 或是參數無效來顯示適當的錯誤訊息。 責任將會落在應用程式的建立者身上，以確保他們了解自己所定義的參數。

若要刪除應用程式，請按一下 `Deployed Apps` 側邊面板中位於應用程式旁邊的垃圾桶按鈕。

## <a name="next-steps"></a>後續步驟

探索如何在您的應用程式[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]中將部署的應用程式與大型資料叢集上的[應用程式](big-data-cluster-consume-apps.md)整合, 以取得詳細資訊。 您也可以參考[應用程式部署範例](https://aka.ms/sql-app-deploy) \(英文\) 中的其他範例，以嘗試搭配此擴充模組使用。

如需有關[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊, 請參閱[ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]什麼是？](big-data-cluster-overview.md)。


我們的目標是使此擴充功能對您有用，並歡迎您提供任何意見反應。 請將它們傳送給 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 小組](https://aka.ms/sqlfeedback)。
