---
title: 準備資料使用 PowerShell （逐步解說） |Microsoft 文件
ms.custom: ''
ms.date: 11/10/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: fbe74b101642ecabe0478a9d5b459e59f277da04
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="prepare-the-data-using-powershell-walkthrough"></a>準備要使用 PowerShell （逐步解說） 的資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

此時，您應該會安裝下列其中之一：

+ SQL Server 2016 R Services
+ SQL Server 2017 機器學習服務，啟用之 R 語言

在這一課，您可以下載資料、 R 封裝和 R 指令碼 Github 儲存機制從逐步解說中使用。 您可以下載使用的 PowerShell 指令碼，以方便使用的所有項目。

您也需要安裝某些其他的 R 封裝，在伺服器和 R 工作站上。 說明的步驟。

然後，您可以使用第二個 PowerShell 指令碼，RunSQL_R_Walkthrough.ps1，設定用來模型化和計分的資料庫。 指令碼執行的程式資料的大量載入到資料庫，並接著會建立一些 SQL 函式和預存程序，可簡化資料科學工作。

讓我們開始吧 ！

## <a name="1-download-the-data-and-scripts"></a>1.下載的資料和指令碼

GitHub 儲存機制中已提供所需的所有程式碼。 您可以使用 PowerShell 指令碼來產生檔案的本機複本。

1.  在資料科學用戶端電腦上，以系統管理員身分開啟 Windows PowerShell 命令提示字元。

2.  若要確保您可以執行下載指令碼而不發生錯誤，請執行此命令。 它會暫時允許指令碼而不需變更系統預設值。

    ```
    Set-ExecutionPolicy Unrestricted -Scope Process -Force
    ```
      
3.  執行下列 Powershell 命令，以將指令碼檔案下載至本機目錄。 如果您未指定不同的目錄，依預設資料夾`C:\tempR`建立及儲存至該處的所有檔案。
  
    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'
    ```
  
    如果您想要將檔案儲存至不同的目錄，請編輯 *DestDir* 參數的值，並指定電腦上的不同資料夾。 如果您輸入資料夾名稱不存在時，PowerShell 指令碼會為您建立的資料夾。
  
4.  下載可能需要一些時間。 完成之後，Windows PowerShell 命令主控台應該如下︰
  
    ![PowerShell 指令碼完成之後](media/rsql-e2e-psscriptresults.PNG "PowerShell 指令碼完成之後")
  
5.  在 PowerShell 主控台中，您可以執行 `ls` 命令，來檢視已下載至 *DestDir*的檔案清單。  如需檔案的說明，請參閱[包含的內容](#What-the-Download-Includes)。

## <a name="2-install-required-r-packages"></a>2.安裝必要的 R 封裝

這個逐步解說需要一些預設不會安裝為 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]一部份的 R 程式庫。 您開發方案，以及上，您必須在用戶端上安裝這兩個封裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您用來部署解決方案的電腦。

### <a name="install-required-packages-on-the-client"></a>在用戶端上安裝必要套件

您所下載的 R 指令碼包含要下載並安裝這些套件的命令。

1. 在 R 環境中，開啟指令碼檔案 (RSQL_R_Walkthrough.R)。

2. 反白顯示並執行下列數行。
    
    ```
    # Install required R libraries, if they are not already installed.
    if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
    if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
    if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
    if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
    ```
    
    有些封裝也會安裝必要的封裝。 總共大約需要 32 個套件。

### <a name="install-required-packages-on-the-server"></a>在伺服器上安裝必要套件

有許多不同的方式，您可以在 SQL Server 上安裝封裝。 例如，SQL Server 提供[封裝管理](../r/installing-and-managing-r-packages.md)功能，可讓資料庫管理員建立的封裝儲存機制，並將使用者指派的權限安裝自己的封裝。 不過，如果您是電腦上的系統管理員，您可以在安裝新的封裝使用 R，只要您將安裝到正確的程式庫。

> [!NOTE]
> 在伺服器上，**不**即使提示您安裝至使用者的文件庫。 如果您安裝至使用者的文件庫時，SQL Server 執行個體無法找到或執行封裝。 如需詳細資訊，請參閱 [在 SQL Server 上安裝新的 R 封裝](../r/install-additional-r-packages-on-sql-server.md)。

1. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上，**以系統管理員身分**開啟 RGui.exe。  如果您已使用預設值來安裝 SQL Server R 服務，則可以在 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64 中找到 RGui.exe。

2.  在 R 提示字元中，執行下列 R 命令：
  
    ```
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    ```

    - 這個範例會使用 R grep 函式，來搜尋可用的路徑的向量，並尋找包含"Program Files"路徑。 如需詳細資訊，請參閱[ http://www.rdocumentation.org/packages/base/functions/grep ](http://www.rdocumentation.org/packages/base/functions/grep)。

    - 如果您認為已安裝的封裝，請檢查已安裝的封裝清單執行`installed.packages()`。

## <a name="3-prepare-the-environment-using-runsqlrwalkthroughps1"></a>3.準備使用 RunSQL_R_Walkthrough.ps1 環境

資料檔、 R 指令碼，以及 T-SQL 指令碼，以及此下載包含 PowerShell 指令碼`RunSQL_R_Walkthrough.ps1`。 指令碼會執行下列動作：

- 確認是否已安裝適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 SQL Native Client 和 SQL 命令列公用程式。 需要有命令列工具，才能執行 [bcp 公用程式](../../tools/bcp-utility.md)，用來將資料快速大量載入至 SQL 資料表。

- 連接到指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，並執行一些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼來設定資料庫以及建立模型和資料的資料表。

- 執行 SQL 指令碼來建立數個預存程序。

- 將您先前下載的資料載入至名稱為 `nyctaxi_sample` 的資料表。

- 重寫 R 指令碼檔案中的引數，以使用您所指定的資料庫名稱。

您用來建置此方案的電腦上執行此指令碼： 例如，膝上型電腦開發和測試您的 R 程式碼的位置。 這部電腦 (我們稱為資料科學用戶端) 必須能夠使用「具名管道」通訊協定連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。

1. 開啟 PowerShell 命令列**以系統管理員身分**。
  
2.  巡覽至您已下載指令碼的資料夾，並輸入所顯示的指令碼名稱。 按 ENTER 鍵。

    ```
    .\RunSQL_R_Walkthrough.ps1
    ```
  
3.  系統提示您針對每個下列參數：
  
    **資料庫伺服器名稱**： 機器學習服務或 R 服務安裝所在的 SQL Server 執行個體的名稱。

    根據您網路的需求，執行個體名稱可能需要限定一或多個子網路名稱。  例如，如果 MYSERVER 無法運作，請嘗試 myserver.subnet.mycompany.com。
    
    **您要建立的資料庫名稱**：例如，您可以輸入 **Tutorial** 或 **Taxi**

    **使用者名稱**：提供具有資料庫存取權限的帳戶。 有兩個選項：
    
    + 輸入具有 CREATE DATABASE 權限的 SQL 登入名稱，然後在後續提示中提供 SQL 密碼。
    + 按 ENTER 鍵而不輸入任何名稱，即使用您自己的 Windows 身分識別，並在安全提示中輸入您的 Windows 密碼。 PowerShell 不支援輸入不同的 Windows 使用者名稱。
    + 如果您無法指定有效的使用者，指令碼會預設為使用整合式的 Windows 驗證。
    
      > [!WARNING]
      > 當您使用 PowerShell 指令碼中的提示來提供認證時，密碼會寫入至更新的指令碼檔案，以純文字。 在您建立所需的 R 物件之後，請立即編輯檔案以移除認證。
      
    **csv 檔案的路徑**：提供資料檔案的完整路徑。 預設的路徑和檔案名稱為 `C:\tempR\nyctaxi1pct.csv`。
  
4.  按 ENTER 執行指令碼。

    指令碼應該會自動下載檔案，並自動將資料載入資料庫。 這可能需要一段時間。 請注意 PowerShell 視窗中的狀態訊息。
      
    如果大量匯入或任何其他步驟失敗，您可以將資料載入以手動方式中所述[疑難排解](#bkmk_Troubleshooting)> 一節。

**結果 (成功完成)**

```
Execution successful
Completed registering all stored procedures used in this walkthrough.
This step (registering all stored procedures) takes 0.39 seconds.
Plug in the database server name, database name, user name and password into the R script file
This step (plugging in database information) takes 0.48 seconds.
```

按一下此連結可跳至下一課：[檢視和瀏覽使用 SQL 資料](/walkthrough-view-and-explore-the-data.md)

## <a name="bkmk_Troubleshooting"></a>疑難排解

如果您有使用 PowerShell 指令碼的任何問題，您可以執行任何或所有步驟以手動方式，使用 PowerShell 指令碼的行，做為範例。 本節列出一些常見的問題及因應措施。

### <a name="powershell-script-didnt-download-the-data"></a>PowerShell 指令碼不會下載資料

若要手動下載資料，以滑鼠右鍵按一下下列連結，然後選取 [另存目標] 。

[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)

記下所下載資料檔案的路徑以及在其中儲存資料的檔案名稱。 您需要將資料載入至資料表使用的完整路徑**bcp**。

### <a name="unable-to-download-the-data"></a>無法下載資料

資料檔案太大。 您必須使用具有相對較佳的網際網路連線的電腦，或可能會逾時下載。

### <a name="could-not-connect-or-script-failed"></a>無法連接，或指令碼失敗

執行某個指令碼時，您可能會收到此錯誤：「建立 SQL Server 的連接時發生網路相關或執行個體特定錯誤」

+ 檢查執行個體名稱的拼寫。
+ 確認完整連接字串。
+ 根據您網路的需求，執行個體名稱可能需要限定一或多個子網路名稱。  例如，如果 MYSERVER 無法運作，請嘗試 myserver.subnet.mycompany.com。
+ 檢查 Windows 防火牆是否允許 SQL Server 的連線。
+ 嘗試登錄您的伺服器，並確定它允許遠端連線。
+ 如果您使用具名執行個體，請啟用 SQL Browser 以便於連線。

### <a name="network-error-or-protocol-not-found"></a>網路錯誤，或找不到通訊協定

+ 確認執行個體支援遠端連接。
+ 確認指定的 SQL 使用者可以遠端連線到資料庫。
+ 在執行個體上啟用「具名管道」。
+ 檢查帳戶的權限。 您指定的帳戶可能沒有建立新資料庫並上傳資料的權限。

### <a name="bcp-did-not-run"></a>bcp 未執行

+ 確認電腦上具有 [bcp 公用程式](../../tools/bcp-utility.md) 。 您可以從 PowerShell 視窗或 Windows 命令提示字元執行 **bcp**。
+ 如果您收到錯誤，請將 **bcp** 公用程式的位置新增至 PATH 系統環境變數，然後再試一次。

### <a name="the-table-schema-was-created-but-the-table-has-no-data"></a>已建立資料表結構描述，但資料表中沒有資料

如果執行指令碼的其餘部分時未發生問題，則您可以從命令列呼叫 **bcp** ，手動將資料上傳至資料表，如下：

#### <a name="using-a-sql-login"></a>使用 SQL 登入

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password>
~~~~

#### <a name="using-windows-authentication"></a>使用 Windows 驗證

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T
~~~~

+ `in`關鍵字會指定資料移動的方向。
+ **-f** 引數會要求您指定格式檔案的完整路徑。 如果您使用 **in** 選項，則需要格式檔案。
+ 如果要使用 SQL 登入執行 bcp，使用 **-U** 和 **-P** 引數。
+ 如果要使用 Windows 整合式驗證，使用 **-T** 引數。

如果指令碼未載入資料，請檢查語法，並確認已經為網路指定正確的伺服器名稱。 例如，如果您連線到具名執行個體，請務必包含任何的子網路及電腦名稱。 請確認登入有執行大量上傳的能力。

### <a name="i-want-to-run-the-script-without-prompts"></a>我想執行指令碼，但不出現提示

您可以使用此範本，利用您環境特有的值，在單一命令列中指定所有參數。

```
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>
```

下列範例會使用 SQL 登入執行指令碼：

```
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv
```

-   使用 *SqlUserName*的認證，連接到指定的執行個體和資料庫。
-   從 *C:\temp\nyctaxi1pct.csv*檔案取得資料。
-   將資料載入至 *dbo.nyctaxi_sample*資料表，此資料表位於名為 *MyServer* 之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的 *MyDB*資料庫中。

### <a name="the-data-loaded-but-it-contains-duplicates"></a>資料已載入，但包含重複項目

如果資料庫包含現有資料表的相同名稱和相同的結構描述， **bcp**插入新的資料，而非覆寫現有的資料複本。

若要避免重複的資料，請再次執行指令碼之前截斷任何現有的資料表。

## <a name="whats-included-in-the-sample"></a>在此範例中包含的內容

當您從 GitHub 儲存機制下載的檔案時，您會得到下列：

+ CSV 格式; 中的資料請參閱[定型和計分資料](#bkmk_data)如需詳細資訊
+ 準備環境所需的 PowerShell 指令碼
+ 使用 bcp 將資料匯入 SQL Server 的 XML 格式檔案
+ 多個 T-SQL 指令碼
+ 您需要用以執行此逐步解說的所有 R 程式碼

### <a name="bkmk_data"></a>定型和計分的資料

資料是包含 2013 年超過 173,000,000 筆個別車程記錄的紐約市計程車資料集的代表性取樣 (包含針對每個車程所付的費用和小費金額)。 為了讓您輕鬆地使用資料，Microsoft 資料科學小組已執行縮小取樣，只取得 1% 的資料。  這項資料已共用於 Azure 中的公用 Blob 儲存容器，格式為 .CSV。 來源資料是壓縮的檔，只在 350 MB。

+ 公用資料集: [NYC 計程車和 Limousine 佣金] (http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)

+ [建立 Azure ML 模型 NYC 計程車資料集](https://blogs.technet.microsoft.com/machinelearning/2015/04/02/building-azure-ml-models-on-the-nyc-taxi-dataset/.

### <a name="powershell-and-r-script-files"></a>PowerShell 和 R 指令碼檔案

+ **RunSQL_R_Walkthrough.ps1**您執行這個指令碼首先，使用 PowerShell。 它會呼叫 SQL 指令碼，以將資料載入至資料庫。

+ **taxiimportfmt.xml** BCP 公用程式用來將資料載入至資料庫中的格式定義檔案。

+ **RSQL_R_Walkthrough.R**這是核心 R 指令碼中進行資料分析和模型的課程的其餘部分使用。 它會提供瀏覽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料、建立分類模型以及建立繪圖所需的所有 R 程式碼。

### <a name="t-sql-script-files"></a>T-SQL 指令碼檔案

PowerShell 指令碼會執行多個[!INCLUDE[tsql](../../includes/tsql-md.md)]SQL Server 執行個體上的指令碼。 下表列出[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼和它們的功用。

|SQL 指令碼檔案名稱|Description|
|------------------------|----------------|
|create-db-tb-upload-data.sql|建立資料庫和兩個資料表：<br /><br /> *nyctaxi_sample*：儲存定型資料的資料表，1% 的 NYC 計程車資料集樣本。 叢集資料行存放區索引會新增至資料表，以提高儲存和查詢效能。<br /><br /> *nyc_taxi_models*： 用來儲存已定型的模型，以二進位格式的資料表。|
|PredictTipBatchMode.sql|建立預存程序，以呼叫所定型的模型來預測新觀測的標籤。 它會接受查詢作為其輸入參數。|
|PredictTipSingleMode.sql|建立預存程序，以呼叫所定型的分類模型來預測新觀測的標籤。 新觀測的變數會傳入為內嵌參數。|
|PersistModel.sql|建立預存程序，以協助將分類模型的二進位表示法儲存在資料庫的資料表中。|
|fnCalculateDistance.sql|建立 SQL 純量值函式，以計算上車與下車位置之間的直線距離。|
|fnEngineerFeatures.sql|建立 SQL 資料表值函數，以建立用於定型分類模型的特徵|

本逐步解說中使用的 T-SQL 查詢已通過測試，並可以當做執行的 R 程式碼中。 不過，如果您想要進一步實驗或開發專屬方案，則建議您先使用專用的 SQL 開發環境來測試和微調查詢，再將它們新增至您的 R 程式碼。

+ 適用於 [Visual Studio Code](https://code.visualstudio.com/) 的 [mssql 擴充功能](https://code.visualstudio.com/docs/languages/tsql)是可以執行查詢的免費、輕量型環境，而且還支援大多數的資料庫開發工作。
+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 是功能強大但免費的工具，可用來開發及管理 SQL Server 資料庫。

## <a name="next-lesson"></a>下一課

[檢視及瀏覽的資料，使用 R 和 SQL](/walkthrough-view-and-explore-the-data.md)

## <a name="previous-lesson"></a>上一課

[R 和 SQL Server 的端對端資料科學逐步解說](/walkthrough-data-science-end-to-end-walkthrough.md)

[資料科學逐步解說的必要條件](walkthrough-prerequisites-for-data-science-walkthroughs.md)
