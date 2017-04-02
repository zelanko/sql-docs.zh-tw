---
title: "在 SQL Server 上安裝其他的 R 封裝 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# 在 SQL Server 上安裝其他的 R 封裝
本主題說明如何安裝新的 R 封裝的執行個體 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 能夠存取網際網路的電腦上。

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1.在 ZIP 檔案格式中找出 Windows 二進位檔案

在許多平台上支援的 R 封裝。 您必須確定您想要安裝的封裝具有二進位格式，以便在 Windows 平台。 否則將無法運作下載的封裝。

例如，從 Bioconductor 取得 [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) 封裝：  
  
1.  在 [Package Archives] (封裝封存)  清單中找到 **Windows 二進位** 版本。  
  
2.  以滑鼠右鍵按一下 .ZIP 檔案的連結，然後選取 [另存目標]  。  
  
3.  瀏覽至本機儲存壓縮封裝的資料夾，按一下 [儲存] 。  
  
 此程序會建立封裝的本機複本。 然後，您可以安裝封裝，或將壓縮的封裝複製到沒有網際網路存取的伺服器。  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2.SQL Server R 服務開啟預設 R 封裝程式庫 

瀏覽至其中的 R 封裝相關聯的伺服器上的資料夾 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 安裝。 請務必要與目前執行個體相關聯的預設程式庫安裝套件。 

如需有關如何尋找此文件庫的指示，請參閱 [安裝和管理的 R 封裝](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。

   針對每個執行個體，您將在其中執行封裝時，您必須安裝個別封裝的複本。 目前封裝無法在執行個體之間共用。
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3.開啟 [系統管理命令提示字元 

以系統管理員身分開啟 R。  您可以使用 Windows 命令 p ropt，或是利用 R 公用程式來執行這項操作。
  
### <a name="using-the-windows-command-prompt"></a>使用 Windows 命令提示字元 

1. 開啟 Windows 命令提示字元，以系統管理員身分，並巡覽至 RTerm.Exe 或 RGui.exe 檔案所在的目錄。  
  
    在預設安裝中，這是 R **\bin** 目錄。 例如，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，R 工具可以在這裡找到︰ 

    **預設執行個體**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **具名執行個體**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. 執行 **R.Exe**。  
  
### <a name="using-the-r-commandline-utilities"></a>使用 R 命令列公用程式 
  
1. 使用 Windows 檔案總管瀏覽至包含 R 工具的目錄。  
  
2. 以滑鼠右鍵按一下 **RGui.exe** 或 **RTerm.exe**, ，然後選取 **系統管理員身分執行**。  
## <a name="4-install-the-package"></a>4.安裝封裝

安裝封裝的 R 命令取決於是否取得封裝從網際網路或從本機的 zip 檔案。  
  
### <a name="install-package-from-internet"></a>從網際網路安裝套件  
  
1.  一般情況下，您可以使用下列命令從 CRAN 或其中一個鏡像站台安裝新的封裝。  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    請注意，封裝名稱一律使用雙引號。

2.  若要指定先安裝套件的程式庫，使用類似的命令設定程式庫位置︰
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    請注意，對於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 、 目前允許只使用一個封裝程式庫。 請勿將封裝安裝至使用者的文件庫，或無法執行封裝的來源 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。   
     
3.  定義文件庫位置之後，下列陳述式會安裝至 R 服務所使用的封裝程式庫常用 e1070 封裝。  
  
    ```  
    install.packages("e1071", lib = lib.SQL)  
    ```  
  
4.  您需要提供取得封裝的鏡像網站。 選取對您位置而言方便的任何鏡像網站。  
  
    如需目前的 CRAN 鏡像清單，請參閱 [這個網站](https://cran.r-project.org/mirrors.html)。  
  
    > [!TIP]  
    >  如果不想每次加入新封裝都要選取鏡像網站，您可以將 R 開發環境設定成一律使用相同的儲存機制。  
    >   
    >  若要這樣做，請編輯全域 R 設定檔 .Rprofile，並加入下行︰  
    >   
    >  `options(repos=structure(c(CRAN="<mirror site URL>")))`  
    >   
    >  如需 R 執行階段啟動時載入的喜好設定和其他檔案的詳細資訊，請從 R 主控台執行這個命令︰  
    >   
    >  `?Startup`  
  
5.  如果目標封裝相依於其他封裝，R 安裝程式就會自動下載相依性，並為您安裝它們。  
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>手動封裝安裝，或無法存取網際網路的電腦上安裝 

1. 如果您想要安裝的封裝相依性，取得事先所需的封裝，並將它們加入至資料夾中，與其他壓縮檔案的封裝。

    > [!TIP]
    > 
    > 我們建議您設定本機儲存機制使用 [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) 如果您需要支援的 R 封裝經常離線安裝。  
  
2.  在 R 命令提示字元中輸入下列命令，指定要安裝的封裝名稱與路徑︰  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    此命令會從其本機 zip 檔案，並假設您將複本儲存在目錄中擷取 R 封裝 `C:\Temp\Downloaded packages`, ，並將 （具有相依性） 的封裝安裝到本機電腦上的 R 程式庫。  
  
3.  如果您先前已修改電腦上的 R 環境，您應該確保 R 環境變數 `.libPath` 會使用指向 R_SERVICES 資料夾執行個體中的單一路徑。  
  
> [!NOTE]
> 如果您已安裝 Microsoft R 伺服器 （獨立） 以及 SQL Server R 服務，您的電腦必須另外安裝 R 的所有 R 工具和文件庫。 僅供 Microsoft R Server R_SERVER 程式庫安裝的封裝，而且無法存取所 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
> 
>  請務必安裝您想要使用 SQL Server 中的封裝時，使用 R_SERVICES 程式庫。

  
## <a name="see-also"></a>另請參閱  
 [設定 SQL Server R 服務 #40; 在資料庫 &#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  