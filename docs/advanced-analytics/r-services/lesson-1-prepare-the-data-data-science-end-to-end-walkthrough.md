---
title: "第 1 課︰準備資料 (資料科學端對端逐步解說) | Microsoft Docs"
ms.custom: ""
ms.date: "03/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: 29
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 25
---
# 第 1 課︰準備資料 (資料科學端對端逐步解說)
若要準備此逐步解說，您需要執行下列動作：

1. 下載要在逐步解說中使用的資料和所有 R 指令碼。 提供 PowerShell 指令碼來簡化從 GitHub 下載。   

2. 在伺服器和您的 R 工作站上，安裝一些額外的 R 封裝。  

3. 準備環境，包括用於模型化和評分的資料庫和資料。
 
    您將基於此目的使用第二個 PowerShell 指令碼 RunSQL_R_Walkthrough.ps1。
    此指令碼會設定資料庫，並將資料上傳至您指定的資料表。  它也會建立一些 SQL 函數與預存程序，以簡化資料科學工作。 
 

## <a name="1-download-the-data-and-scripts"></a>1.下載資料和指令碼  
GitHub 存放庫中已提供完成這個逐步解說所需的所有程式碼。 您可以使用 PowerShell 指令碼來產生檔案的本機複本。  
  
#### <a name="to-download-all-scripts-using-powershell"></a>使用 PowerShell 下載所有指令碼  
  
1.  在資料科學用戶端電腦上，以系統管理員身分開啟 Windows PowerShell 命令提示字元。  
  
2.  如果您之前未在這個執行個體上執行過 PowerShell，或沒有執行指令碼的權限，則可能會遇到錯誤。 如果是這樣，請先執行這個命令，再執行指令碼，以暫時允許指令碼，而不需要變更系統預設值。  
  
    ```  
    Set-ExecutionPolicy Unrestricted -Scope Process -Force  
    ```  
  
3.  執行下列命令，以將指令碼檔案下載至本機目錄。 如果您未指定不同的目錄，預設會建立 C:\tempR 資料夾，並在該處儲存所有檔案。  
  
    ```  
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'  
  
    ```  
  
    如果您想要將檔案儲存至不同的目錄，請編輯 *DestDir* 參數的值，並指定電腦上的不同資料夾。 如果您輸入不存在的資料夾名稱，PowerShell 指令碼將為您建立資料夾。  
  
4.  下載完成之後，Windows PowerShell 命令主控台應該如下︰  
  
    ![After completion of PowerShell script](../../advanced-analytics/r-services/media/rsql-e2e-psscriptresults.PNG "After completion of PowerShell script")  
  
5.  在 PowerShell 主控台中，您可以執行 `ls` 命令，來檢視已下載至 *DestDir* 的檔案清單。  如需檔案的清單和說明，請參閱[包含的內容](#What-the-Download-Includes)。
  
## <a name="2-install-required-packages"></a>2.安裝必要套件  
這個逐步解說需要一些預設不會安裝為 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 一部份的 R 程式庫。 您必須在要於其中開發方案的用戶端上以及要在其中部署方案的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上，安裝套件。  
  
### <a name="install-required-packages-on-the-client"></a>在用戶端上安裝必要套件  
您所下載的 R 指令碼包含要下載並安裝這些套件的命令。  
  
1.  在 R 環境中，開啟指令碼檔案 (RSQL_R_Walkthrough.R)。  
  
2.  反白顯示並執行下列數行。  
  
    ```  
    # Install required R libraries for this walkthrough if they are not installed.   
  
    if (!('ggmap' %in% rownames(installed.packages()))){  
      install.packages('ggmap')  
    }  
    if (!('mapproj' %in% rownames(installed.packages()))){  
      install.packages('mapproj')  
    }  
    if (!('ROCR' %in% rownames(installed.packages()))){  
      install.packages('ROCR')  
    }  
    if (!('RODBC' %in% rownames(installed.packages()))){  
      install.packages('RODBC')  
    }  
    ```  
  
### <a name="install-required-packages-on-the-server"></a>在伺服器上安裝必要套件  

  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上，以系統管理員身分開啟 RGui.exe。  如果您已使用預設值來安裝 SQL Server R 服務，則可以在 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64 中找到 RGui.exe。  
  
    或者，如果您已在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上安裝其他 R 環境 (例如 RStudio)，則可以使用 R 主控台來執行命令。  
  
2.  在 R 提示字元中，執行下列 R 命令：  
  
    ```  
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])  
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    ```  
  
**注意：**  
  
-   這個範例會使用 R grep 函數來搜尋可用路徑的向量，並在 “Program Files” 中尋找路徑。 如需詳細資訊，請參閱 [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep)。   
  
-   如果您認為已經安裝封裝，請使用 R 函數 `installed.packages()` 來檢查已安裝的封裝清單。  
  
-   如果您無法寫入 Program Files 中的主要程式庫，可在用戶端上安裝至使用者程式庫。 不過，將封裝安裝至 SQL Server 電腦時，您必須在 SQL Server R 服務所使用的預設程式庫中安裝它們。 請勿使用使用者程式庫。 如需詳細資訊，請參閱[在 SQL Server 上安裝新的 R 封裝](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)。
      

## <a name="3-run-powershell-script-runsqlrwalkthroughps1"></a>3.執行 Powershell 指令碼 RunSQL_R_Walkthrough.ps1  

您可以在將建置方案的電腦上執行這個 PowerShell 指令碼，例如，電腦開發和測試您的 R 程式碼。 這部電腦必須可以使用具名管道通訊協定連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。  
  
指令碼會執行下列動作：  
  
-   確認是否已安裝適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 SQL Native Client 和 SQL 命令列公用程式。 需要有命令列工具，才能執行 [bcp 公用程式](../../tools/bcp-utility.md)，以用於將資料快速大量載入至 SQL 資料表。    
-   連接到指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，並執行一些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼來設定資料庫以及建立模型和資料的資料表。    
-   執行 SQL 指令碼來建立數個預存程序。    
-   將您先前下載的資料載入至資料表 nyctaxi_sample。    
-   重寫 R 指令碼檔案中的引數，以使用您所指定的資料庫名稱。 

### <a name="to-run-the-script"></a>執行指令碼
  
1.  以系統管理員身分開啟 PowerShell 命令列。    
  
2.  巡覽至您已下載指令碼的資料夾，並輸入所顯示的指令碼名稱。 按 ENTER 鍵。  
  
    ```  
    .\RunSQL_R_Walkthrough.ps1  
    ```  
  
3.  系統會提示您輸入下列所有參數：  
  
    - 您想要建立的資料庫名稱。 
      例如，您可以輸入 **Tutorial** 或 **Taxi**  
    - 用來執行指令碼的認證。 有兩個選項：
        + 輸入具有 CREATE DATABASE 權限的 SQL 登入名稱，然後在後續提示中提供 SQL 密碼。
        + 按 ENTER 鍵，而不輸入任何名稱來使用您自己的 Windows 身分識別，並在安全提示中輸入您的 Windows 密碼。 PowerShell 不支援輸入不同的 Windows 使用者名稱。 

          如果您無法指定有效的使用者，指令碼預設將使用整合式 Windows 驗證。  
  
    -   您想要上傳至資料庫的 CSV 檔案完整路徑  
  
        指令碼應該會下載檔案，並自動將資料載入至資料庫，但是，如果失敗，您一律可以手動上傳資料。  
  
4.  按 ENTER 執行指令碼。  
  
## <a name="troubleshooting"></a>疑難排解  
 
 如果您遇到問題時，您可以使用 PowerShell 指令碼行做為範例，手動執行全部或任何步驟。 
 

### <a name="the-powershell-script-didnt-download-the-data"></a>PowerShell 指令碼不會下載資料
  
若要手動下載資料，以滑鼠右鍵按一下下列連結，然後選取 [另存目標]。  
  
[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)  
  
記下所下載資料檔案的路徑以及在其中儲存資料的檔案名稱。 您需要這個路徑，使用 **bcp**將資料載入至資料表。  
  
### <a name="i-was-unable-to-download-the-data"></a>我無法下載資料
資料檔案太大。 使用網際網路連接相對較佳的電腦，或者下載可能逾時。  

  
### <a name="could-not-connect-or-script-failed"></a>無法連接，或指令碼失敗  
  
+ 檢查執行個體名稱的拼寫。 
+ 確認完整連接字串。    
+ 根據您網路的需求，執行個體名稱可能需要限定一或多個子網路名稱。  例如，如果 MYSERVER 無法運作，請嘗試 myserver.subnet.mycompany.com。
  
### <a name="network-error-or-protocol-not-found"></a>網路錯誤，或找不到通訊協定  
  
+ 確認執行個體支援遠端連接。    
+ 確認指定的 SQL 使用者可以從遠端連接至資料庫，而且執行個體上已啟用具名管道。    
+ 檢查帳戶的權限。 您指定的帳戶可能沒有建立新資料庫並上傳資料的權限。  

### <a name="bcp-did-not-run"></a>bcp 未執行  

+ 確認電腦上具有 [bcp 公用程式](../../tools/bcp-utility.md)。 您可以從 PowerShell 視窗或 Windows 命令提示字元執行 bcp。
+ 如果您收到錯誤，請將 bcp 公用程式的位置新增至 PATH 系統環境變數，然後再試一次。  

### <a name="the-table-schema-was-created-but-there-is-no-data-in-the-table"></a>已建立資料表結構描述，但資料表中沒有資料

如果執行指令碼的其餘部分時未發生問題，則您可以從命令列呼叫 **bcp**，手動將資料上傳至資料表，如下：  


 
**使用 SQL 登入**
    
~~~~ 
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password  
~~~~  
  
**使用 Windows 驗證**  

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T 
~~~~ 
  
  
+ **in** 關鍵字會指定資料移動的方向。  
+ **-f** 引數會要求您指定格式檔案的完整路徑。 如果您使用 **in** 選項，則需要格式檔案。
+ 如果要使用 SQL 登入執行 bcp，使用 **-U** 和 **-P** 引數。
+ 如果要使用 Windows 整合式驗證，使用 **-T** 引數。 

  
### <a name="how-can-i-run-the-script-without-prompts"></a>我如何在執行指令碼時不出現提示？  
  
您可以利用您環境特有的值，在單一命令列中指定所有參數。 
  
```  
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>  
```  
  
例如，若要使用 SQL 登入執行指令碼：  
  
```  
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv  
```  
  
此範例會執行下列各項：  
  
-   使用 *SqlUserName* 的認證，連接到指定的執行個體和資料庫。  
-   從 *C:\temp\nyctaxi1pct.csv* 檔案取得資料。  
-   將資料載入至 *dbo.nyctaxi_sample* 資料表，此資料表位於名為 *MyServer* 之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的 *MyDB* 資料庫中。  

### <a name="the-data-loaded-but-it-contains-duplicates"></a>資料已載入，但包含重複項目

如果資料表已存在，而且具有正確的結構描述，bcp 將會繼續執行，但將插入資料的新複本，而非覆寫現有的資料。 這會導致資料重複。  請務必截斷任何現有的資料表，然後重新執行指令碼。

## <a name="what-the-download-includes"></a>下載所包含的內容

當您從 GitHub 儲存機制下載檔案時，您將會得到以下各項：
+ CSV 格式的資料
+ 準備環境所需的 PowerShell 指令碼
+ 使用 bcp 將資料匯入 SQL Server 的 XML 格式檔案
+ 多個 T-SQL 指令碼
+ 您需要用以執行此逐步解說的所有 R 程式碼

### <a name="training-and-scoring-data"></a>為資料定型和計分  
資料是包含 2013 年超過 173,000,000 筆個別車程記錄的紐約市計程車資料集的代表性取樣 (包含針對每個車程所付的費用和小費金額)。  如需一開始如何收集此資料以及如何取得完整資料集的詳細資訊，請參閱  
[http://chriswhong.com/open-data/foil_nyc_taxi/](http://chriswhong.com/open-data/foil_nyc_taxi/)。  
  
為了讓您輕鬆地使用資料，Microsoft 資料科學小組已執行縮小取樣，只取得 1% 的資料。  這項資料已共用於 Azure 中的公用 Blob 儲存容器，格式為 .CSV。 來源資料是未壓縮檔案，低於 350 MB。  
 
### <a name="files"></a>檔案

 
+ **RunSQL_R_Walkthrough.ps1** 您會先使用 PowerShell 來執行這個指令碼。 它會呼叫 SQL 指令碼，以將資料載入至資料庫。  
    
+ **taxiimportfmt.xml** BCP 公用程式用來將資料載入至資料庫中的格式定義檔案。
      
+ **RSQL_R_Walkthrough.R** 這是核心 R 指令碼，將用於執行資料分析和模型化之課程的其餘部分。 它會提供瀏覽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料、建立分類模型以及建立繪圖所需的所有 R 程式碼。   
  
### <a name="sql-scripts"></a>SQL 指令碼  
這個 PowerShell 指令碼會在伺服器上執行多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 下表列出 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案。  
  
|SQL 指令碼檔案名稱|用途|  
|------------------------|----------------|  
|create-db-tb-upload-data.sql|建立資料庫和兩個資料表：<br /><br /> *nyctaxi_sample*：儲存定型資料的資料表，1% 的 NYC 計程車資料集樣本。 叢集資料行存放區索引會新增至資料表，以提高儲存和查詢效能。<br /><br /> *nyc_taxi_models*：稍後將用來儲存所定型分類模型的空白資料表。|  
|PredictTipBatchMode.sql|建立預存程序，以呼叫所定型的模型來預測新觀測的標籤。 它會接受查詢作為其輸入參數。|  
|PredictTipSingleMode.sql|建立預存程序，以呼叫所定型的分類模型來預測新觀測的標籤。 新觀測的變數會傳入為內嵌參數。|  
|PersistModel.sql|建立預存程序，以協助將分類模型的二進位表示法儲存在資料庫的資料表中。|  
|fnCalculateDistance.sql|建立 SQL 純量值函式，以計算上車與下車位置之間的直線距離。|  
|fnEngineerFeatures.sql|建立 SQL 資料表值函數，以建立用於定型分類模型的特徵|  
  
這個逐步解說中使用的所有 SQL 查詢都已經過測試，並且可以依現狀在 R 程式碼中執行。 不過，如果您想要使用 SQL 查詢進一步實驗或開發專屬方案，則建議您先使用開發環境 (例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ) 來測試和微調查詢，再將它們新增至您的 R 程式碼。  
  
  
## <a name="next-lesson"></a>下一課  
[第 2 課︰檢視和瀏覽資料 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>上一課  
[資料科學端對端逐步解說](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
  
  
