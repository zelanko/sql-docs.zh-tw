---
title: "在 SQL Server 上安裝其他的 R 套件 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: adc0e5fc229547632759c5702e98d87f4b71cbb3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="install-additional-r-packages-on-sql-server"></a>在 SQL Server 上安裝其他的 R 封裝
本主題說明如何在能夠存取網際網路的電腦上，將新的 R 套件安裝到 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 的執行個體。

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1.找出 ZIP 檔案格式的 Windows 二進位檔

許多平台都支援 R 套件。 您必須確定您想要安裝的套件具有適用於 Windows 平台的二進位格式。 否則，所下載的套件將無法運作。

例如，從 Bioconductor 取得 [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) 封裝：  
  
1.  在 [Package Archives] \(封裝封存)  清單中找到 **Windows 二進位** 版本。  
  
2.  以滑鼠右鍵按一下 .ZIP 檔案的連結，然後選取 [另存目標]  。  
  
3.  瀏覽至本機儲存壓縮封裝的資料夾，按一下 [儲存] 。  
  
 此程序會建立套件的本機複本。 接著，您便可以安裝該套件，或是將壓縮的套件複製到無法存取網際網路的伺服器。  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2.開啟 SQL Server R Services 的預設 R 套件程式庫 

瀏覽至伺服器上已安裝與 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 關聯之 R 套件的資料夾。 請務必將套件安裝到與目前執行個體關聯的預設程式庫。 

如需有關如何找出此程式庫的指示，請參閱[安裝和管理 R 套件](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。

   針對您將執行套件的每個執行個體，您必須安裝個別的套件複本。 目前套件並無法跨執行個體共用。
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3.開啟系統管理命令提示字元 

以系統管理員身分開啟 R。  您可以使用 Windows 命令提示字元，或使用其中一個 R 公用程式，來執行這項操作。
  
### <a name="using-the-windows-command-prompt"></a>使用 Windows 命令提示字元 

1. 以系統管理員身分開啟 Windows 命令提示字元，然後瀏覽至 RTerm.Exe 或 RGui.exe 檔案所在的目錄。  
  
    在預設安裝中，這是 R **\bin** 目錄。 例如，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，R 工具的位置如下： 

    **預設執行個體**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **具名執行個體**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. 執行 **R.Exe**。  
  
### <a name="using-the-r-command-line-utilities"></a>使用 R 命令列公用程式 
  
1. 使用 Windows 檔案總管瀏覽至包含 R 工具的目錄。  
  
2. 在 [RGui.exe] 或 [RTerm.exe] 上按一下滑鼠右鍵，然後選取 [以系統管理員身分執行]。  
## <a name="4-install-the-package"></a>4.安裝套件

用於安裝套件的 R 命令取決於您是要從網際網路取得套件，還是要從本機壓縮檔取得套件。  
  
### <a name="install-package-from-internet"></a>從網際網路安裝套件  
  
1.  一般而言，您會使用下列命令，從 CRAN 或其中一個鏡像站台安裝新套件。  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    請注意，封裝名稱一律使用雙引號。

2.  若要指定應安裝套件的程式庫，請使用類似以下的命令來設定程式庫位置：
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    請注意，針對 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，目前僅允許一個套件程式庫。 請勿將套件安裝到使用者程式庫，否則您將無法從 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行套件。   
     
3.  定義程式庫位置之後，以下陳述式會將常用的 e1070 套件安裝到 R Services 所使用的套件程式庫。  
  
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
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>手動安裝套件或在無法存取網際網路的電腦上安裝 

1. 如果您想要安裝的套件具有相依項目，請事先取得所需的套件，然後將它們新增到含有其他套件壓縮檔的資料夾。

    > [!TIP]
    > 
    > 如果您需要支援頻繁的 R 套件離線安裝，建議您使用 [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) 來設定本機儲存機制。  
  
2.  在 R 命令提示字元中輸入下列命令，指定要安裝的封裝名稱與路徑︰  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    這個命令會從本機 ZIP 壓縮檔案解壓縮 R 封裝，假設您的複本儲存在目錄 `C:\Temp\Downloaded packages`，然後將封裝 (及其相依性) 安裝到本機電腦的 R 程式庫。  
  
3.  如果您先前已修改電腦上的 R 環境，您應該確保 R 環境變數 `.libPath` 僅使用一個路徑，此路徑指向執行個體的 R_SERVICES 資料夾。  
  
> [!NOTE]
> 如果除了 SQL Server R Services 之外，您還安裝了 Microsoft R Server (獨立式)，您的電腦將會有含有所有 R 工具和程式庫的個別 R 安裝。 安裝到 R_SERVER 程式庫的套件僅供 Microsoft R Server 使用，而無法供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取。  
> 
>  安裝您想要在 SQL Server 中使用的套件時，請務必使用 R_SERVICES 程式庫。

  
## <a name="see-also"></a>另請參閱  
 [設定 SQL Server R Services &#40;資料庫內&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  

