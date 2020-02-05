---
title: 應用程式部署擴充功能
titleSuffix: SQL Server big data clusters
description: 在 SQL Server 巨量資料叢集上將 Python 或 R 指令碼部署為應用程式。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e05fa19c8453418c22829862801c5044e6c25d2b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "73707145"
---
# <a name="how-to-use-visual-studio-code-to-deploy-applications-to-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>如何使用 Visual Studio Code 將應用程式部署至 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何使用 Microsoft Visual Studio Code 搭配「應用程式部署」延伸模組，將應用程式部署到 SQL Server 巨量資料叢集。

## <a name="prerequisites"></a>Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/)
- [SQL Server 巨量資料叢集](big-data-cluster-overview.md)

## <a name="capabilities"></a>功能

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

首先，在 Visual Studio Code 中安裝「應用程式部署」延伸模組：

1. 下載[應用程式部署延伸模組](https://aka.ms/app-deploy-vscode) \(英文\) 以將該延伸模組安裝為 Visual Studio Code 的一部分。

1. 啟動 Visual Studio Code 並瀏覽至 [延伸模組] 提要欄位。

1. 按一下提要欄位頂端的 `…` 內容功能表，然後選取 `Install from vsix`。

   ![安裝 VSIX](media/vs-extension/install_vsix.png)

1. 找到您所下載的 `sqlservbdc-app-deploy.vsix` 檔案，然後選擇它以安裝。

安裝 SQL Server 巨量資料叢集應用程式部署延伸模組之後，系統會提示您重新載入 Visual Studio Code。 您現在應該會在 Visual Studio Code 提要欄位中看見 [SQL Server BDC 應用程式總管]。

### <a name="app-explorer"></a>應用程式總管

在提要欄位中按一下該擴充功能，以載入顯示 [應用程式總管] 的側邊面板。 下列的 [應用程式總管] 範例螢幕擷取畫面沒有顯示任何應用程式或應用程式規格：

![應用程式總管](media/vs-extension/app_explorer.png)

#### <a name="connect-to-cluster"></a>連線至叢集

若要連線至叢集端點，請使用下列其中一種方法：

- 按一下位於底部且顯示為 `SQL Server BDC Disconnected`的狀態列。
- 或是按一下位於頂端且具有指向門內箭號的 `Connect to Cluster` 按鈕。

Visual Studio Code 會提示輸入適當的端點、使用者名稱及密碼。

要連線的端點是連接埠為 30080 的 `Cluster Management Service` 端點。

您也可以從命令列透過下列方式尋找此端點 

```
azdata bdc endpoint list
```

取得此資訊的另一種方法是在 Azure Data Studio 中，於伺服器的 [管理]  上按一下滑鼠右鍵，您將在其中找到所列服務的端點。

![ADS 端點](media/vs-extension/ads_end_point.png)

在您找到要使用的端點之後，接著連線至該叢集。

![新增連線](media/vs-extension/connect_to_cluster.png)

 如果所提供的認證及應用程式端點皆正確，Visual Studio Code 會通知您已經連線到叢集，且您將會看見提要欄位中填入所有已部署的應用程式。 如果您成功連線，您的端點和使用者名稱將會作為您使用者設定檔的一部分被儲存到 `./sqldbc`。 系統一律不會儲存密碼或權杖。 再次登入時，系統提示將會預先填入您已儲存的主機和使用者名稱，但一律會要求您輸入密碼。 如果您想要連線到不同的叢集端點，請再次按一下 `New Connection`。 如果您關閉 Visual Studio Code 或開啟不同的工作區，連線將會自動關閉，且您將必須重新連線。

### <a name="app-template"></a>應用程式範本

您必須在 Visual Studio Code 中「開啟工作區」  ，這是您將儲存應用程式成品的位置。

若要利用我們的其中一個範本來部署新的應用程式，請按一下 `New App Template` 窗格上的 `App Specifications` 按鈕；系統將會提示您輸入名稱、執行階段，以及您想要在本機電腦上放置新應用程式的位置。 您所提供的名稱與版本應該是 DNS-1035 標籤，且必須包含小寫英數字元或 '-'、以字母字元開頭，並以英數字元結尾。

建議您將它置於目前的 Visual Studio Code 工作區中，以便使用延伸模組的完整功能，但您可以將它置於本機檔案系統中的任何位置。

![新增應用程式範本](media/vs-extension/new_app_template.png)

完成後，系統會在您所指定的位置對新的應用程式範本進行 Scaffold，且 `spec.yaml` 部署會在您的工作區中開啟。 如果您所選取的目錄是位於您的工作區中，您也應該確定它已列於 `App Specifications` 窗格底下：

![已載入應用程式範本](media/vs-extension/loading_app_template.png)

此範本是一個在 [應用程式規格] 窗格中以下列方式配置的簡單 `helloworld` 應用程式：

- **spec.yaml**
   - 告訴叢集部署您應用程式的方式
- **run-spec.yaml**
   - 告訴叢集您想要呼叫應用程式的方式

應用程式的原始程式碼會在 [工作區] 資料夾中。

- **來源檔案名稱**
   - 這是您的原始程式碼檔案，如 `src` 中的 `spec.yaml` 所指定
   - 它具有稱為 `handler` 的單一函式，其會被視為應用程式的 `entrypoint`，如 `spec.yaml` 中所示。 它會接受名為 `msg` 的字串輸入，並會傳回名為 `out` 的字串輸出。 這些是在 `inputs` 的 `outputs` 和 `spec.yaml` 中指定。

如果您不想要已進行 Scaffold 的範本，且只想要 `spec.yaml` 來部署您已建置的應用程式，請按一下 `New Deploy Spec` 按鈕旁邊的 `New App Template` 按鈕，然後完成相同的程序；在此情況下，您只會接收到 `spec.yaml`，其可供您視需要修改。

### <a name="deploy-app"></a>部署應用程式

您可以透過 `Deploy App` 中的 CodeLens `spec.yaml`，或是按下 [應用程式規格] 功能表中位於 `spec.yaml` 檔案旁邊的閃電資料夾按鈕，來立即部署此應用程式。 擴充功能會將 `spec.yaml` 所在目錄中的所有檔案壓縮，並將應用程式部署到叢集。 

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
- version
- 輸入參數
- 輸出參數
- 連結
  - Swagger
  - 詳細資料

如果您按一下 `Links`，您將會發現您可以存取已部署應用程式的 `swagger.json`，因此您可以自行撰寫會呼叫您應用程式的用戶端：

![Swagger](media/vs-extension/swagger.png)

請參閱[取用巨量資料叢集上的應用程式](big-data-cluster-consume-apps.md)以取得詳細資訊。

### <a name="app-run"></a>應用程式執行

應用程式就緒之後，請使用應用程式範本隨附的 `run-spec.yaml` 來呼叫應用程式：

![執行規格](media/vs-extension/run_spec.png)

指定您想要用來取代 `hello` 的任何字串，然後再次透過 CodeLens 連結，或是提要欄位中位於 `run-spec.yaml` 旁邊的閃電按鈕來執行它。 如果您基於任何原因而沒有執行規格，請從叢集中的已部署應用程式產生一個：

![取得執行規格](media/vs-extension/get_run_spec.png)

在您取得執行規格並依照您的需求編輯它之後，請執行它。 Visual Studio Code 會在應用程式執行完畢時，傳回適當的回饋：

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

若要探索如何在自己的應用程式中整合部署在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上的應用程式，請參閱[取用巨量資料叢集上的應用程式](big-data-cluster-consume-apps.md)以取得詳細資訊。 您也可以參考[應用程式部署範例](https://aka.ms/sql-app-deploy) \(英文\) 中的其他範例，以嘗試搭配此擴充模組使用。

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。


我們的目標是使此擴充功能對您有用，並歡迎您提供任何意見反應。 請將它們傳送給 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 小組](https://aka.ms/sqlfeedback)。
