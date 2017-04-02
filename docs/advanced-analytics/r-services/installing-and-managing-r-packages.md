---
title: "安裝和管理的 R 封裝 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 安裝和管理的 R 封裝
 在執行任何 R 方案 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 必須使用安裝在預設 R 程式庫中的封裝。 更一般來說，R 解決方案會參考使用者的程式庫中的 R 程式碼中，指定檔案路徑，但不是建議用於生產環境。

因此，它是資料庫管理員或其他伺服器上的系統管理員確認已安裝所有必要的套件的工作 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體。 如果您沒有系統管理權限的電腦上裝載 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]  執行個體，您可以提供有關如何安裝 R 封裝的系統管理員資訊並提供存取的安全封裝儲存機制，可取得使用者所要求的封裝。 本節提供這些資訊。 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 提供安裝和管理，讓資料庫管理員和資料科學家更自由和控制封裝使用情形，以及安裝 R 封裝的新功能。 如需詳細資訊，請參閱 [SQL Server 的 R 封裝管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。 

## <a name="installed-packages"></a>已安裝的封裝
當您安裝  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)],  ，根據預設 R **基底** 安裝套件，例如 `stats` 和 `utils`, 連同 **RevoScaleR** 封裝支援連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 
> [!NOTE]  
>  如需預設安裝的封裝，請參閱 [封裝安裝 Microsoft R open](https://mran.microsoft.com/rro/installed/)。  

 如果您需要從 CRAN 或另一個儲存機制的其他封裝，您必須下載套件，並將它安裝在您的工作站。  
  
 如果您需要在伺服器的內容中執行新的封裝時，系統管理員必須安裝它以及在伺服器上。   
   
## <a name="where-and-how-to-get-new-packages"></a>取得新封裝的位置和方法  
 有多個來源可取得 R 封裝，中其最廣為人知的是 CRAN 和 Bioconductor。 R 語言的官方網站 ([https://www.r-project.org/](https://www.r-project.org/)) 會列出這些資源。 許多封裝也會發佈到 GitHub，您可以在這裡取得原始程式碼。 不過，可能提供您已由公司中的某人所開發的 R 封裝。  
  
 不論來源為何，封裝格式必須是要安裝的 ZIP 檔案。 此外，若要使用的套件 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，務必要取得 Windows 二進位格式的壓縮的檔。 （有些封裝可能不支援此格式）。建議的 zip 檔格式，以及如何建立 R 封裝內容的相關詳細資訊，如本教學課程，您可以下載 PDF 格式從 R 專案網站︰ [Freidrich Leisch︰ 建立 R 封裝](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)。 
  
 一般而言，R 封裝可以安裝輕鬆地從命令列而不需要事先下載這些電腦可以存取網際網路。  通常這不是執行伺服器的情況 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 。  因此，將 R 封裝安裝到沒有電腦 **不** 能夠存取網際網路，您必須下載套件的事先壓縮格式正確，然後將 zip 的檔案複製到電腦存取的資料夾。 
 
 下列主題將描述兩個方法來安裝封裝離線︰ 

+ [建立離線封裝儲存機制使用 miniCRAN](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)

  描述如何使用 R 封裝 **miniCRAN** 建立離線的儲存機制。 如果您需要安裝套件的多個伺服器，並從單一位置管理儲存機制，這是可能最有效率的方法。 
+ [從網際網路安裝新的 R 封裝](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)

  包含安裝套件離線壓縮的檔案手動複製的指示。   

## <a name="permissions-required-for-installing-r-packages"></a>安裝 R 封裝所需的權限  
  
若要在執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的電腦上安裝新的 R 封裝，您必須擁有電腦的系統管理權限。   

如果沒有這些權限，請連絡您的系統管理員，並提供要安裝封裝的相關資訊。  
  

如果您做 R 工作站電腦上安裝新的 R 封裝，而且電腦會執行 **不** 擁有執行個體 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝，您仍然需要系統管理權限的電腦以安裝封裝。 安裝封裝之後，您就可以在本機執行封裝。  
 
> [!NOTE]
> 在 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], ，已加入新的資料庫角色來支援封裝的安裝權限的執行個體層級和資料庫層級的範圍。 如需詳細資訊，請參閱 [SQL Server 的 R 封裝管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。
 

### <a name="location-of-default-r-library-location-for-r-services"></a>預設 R R 服務程式庫位置的位置

如果您已安裝  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用預設執行個體，執行個體所使用的 R 封裝程式庫位於 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體資料夾。 例如： 

+ 預設執行個體 _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ 具名執行個體 _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


您可以執行下列陳述式來確認目前的執行個體皆可藉由預設程式庫 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

如需詳細資訊，請參閱 [判斷其套件安裝在 SQL Server](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md)。

## <a name="managing-installed-packages"></a>管理已安裝的套件

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 提供安裝和管理，讓資料庫管理員和資料科學家更自由和控制封裝使用情形，以及安裝 R 封裝的新功能。 如需詳細資訊，請參閱 [SQL Server 的 R 封裝管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。 

如果您使用 SQL Server 2106 R 服務，新的封裝管理功能沒有這一次。 在此同時，您有下列選項，以判斷上已安裝哪些封裝 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦、 使用其中一個選項︰

+ 如果您有權限的資料夾，檢視的預設程式庫。
+ 從 R 命令來列出 R_SERVICES 程式庫位置中的封裝執行的命令
+ 執行個體上使用的預存程序，如下所示︰
   ```SQL
   EXECUTE sp_execute_external_script  @language=N'R'  
        ,@script = N'str(OutputDataSet);  
        packagematrix <- installed.packages();  
        NameOnly <- packagematrix[,1];  
        OutputDataSet <- as.data.frame(NameOnly);'  
        ,@input_data_1 = N'SELECT 1 as col'  
        WITH RESULT SETS ((PackageName nvarchar(250) ))   
   ```


 ## <a name="see-also"></a>另請參閱  
 [管理和監控 R 解決方案](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  