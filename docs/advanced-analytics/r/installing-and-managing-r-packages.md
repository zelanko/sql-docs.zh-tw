---
title: "安裝和管理 R 套件 | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ae30bfc42e42b69158dbba5a38b0bccbe93523b4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="installing-and-managing-r-packages"></a>安裝和管理 R 套件
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中執行的任何 R 方案都必須使用預設 R 程式庫中安裝的套件。 更一般來說，R 方案會透過在 R 程式碼中指定檔案路徑來參考使用者程式庫，但不建議使用於生產環境。

因此，伺服器上的資料庫系統管理員或其他系統管理員必須確保所有必要的套件都已安裝在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體上。 如果您沒有裝載 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體之電腦的系統管理權限，您可以提供系統管理員有關如何安裝 R 套件的資訊，並提供安全套件存放庫的存取權，其中可取得使用者要求的套件。 本節提供該資訊。 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 提供用來安裝及管理 R 套件的新功能，可讓資料庫系統管理員和資料科學家兩者對套件使用情形和安裝，有更充分的自由和控制權。 如需詳細資訊，請參閱 [SQL Server 的 R 套件管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。 

## <a name="installed-packages"></a>已安裝的套件
當您安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 時，根據預設 R **基底**套件 (例如 `stats` 和 `utils`) 會和支援連線至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 **RevoScaleR** 套件一起安裝。  
  
 
> [!NOTE]  
>  如需預設安裝之套件的清單，請參閱[隨 Microsoft R Open 安裝的套件 (英文)](https://mran.microsoft.com/rro/installed/)。  

 如果您需要來自 CRAN 或另一個存放庫的其他套件，您必須下載套件，並在您的工作站上安裝。  
  
 如果您需要在伺服器的內容中執行新的套件，系統管理員也必須在伺服器上安裝該套件。   
   
## <a name="where-and-how-to-get-new-packages"></a>取得新封裝的位置和方法  
 有多個來源可取得 R 封裝，中其最廣為人知的是 CRAN 和 Bioconductor。 R 語言的官方網站 ([https://www.r-project.org/](https://www.r-project.org/)) 會列出許多這些資源。 許多封裝也會發佈到 GitHub，您可以在這裡取得原始程式碼。 不過，可能提供您已由公司中的某人所開發的 R 封裝。  
  
 不論來源為何，封裝格式必須是要安裝的 ZIP 檔案。 此外，若要使用套件搭配 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，請務必取得 Windows 二進位檔案格式的壓縮檔 (部分套件可能不支援此格式)。如需有關壓縮檔格式的內容，以及如何建立 R 套件的詳細資訊，建議您參考此教學課程，您可以從 R 專案網站下載 PDF 格式：[Freidrich Leisch：建立 R 套件 (英文)](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)。 
  
 一般而言，如果電腦可以存取網際網路，R 套件可以輕鬆地從命令列安裝，而不需要事先下載。  通常這不是執行 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 之伺服器的情況。  因此，若要將 R 套件安裝到「無法」存取網際網路的電腦，您必須事先以正確的壓縮檔格式下載套件，並將壓縮檔複製到電腦可存取的資料夾。 
 
 下列主題將說明離線安裝套件的兩個方法： 

+ [使用 miniCRAN 建立離線套件存放庫](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)

  描述如何使用 R 套件 **miniCRAN** 建立離線存放庫。 如果您需要將套件安裝到多部伺服器並從單一位置管理存放庫，這可能是最有效率的方法。 
+ [從網際網路安裝新的 R 套件](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)

  包含手動複製壓縮檔來離線安裝套件的指示。   

## <a name="permissions-required-for-installing-r-packages"></a>安裝 R 封裝所需的權限  
  
若要在執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的電腦上安裝新的 R 套件，您必須擁有電腦的系統管理權限。   

如果沒有這些權限，請連絡您的系統管理員，並提供要安裝封裝的相關資訊。  
  

如果新的 R 套件是安裝在做為 R 工作站使用的電腦上，而且該電腦「沒有」安裝 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的執行個體，您仍需要有電腦的系統管理權限才能安裝套件。 安裝封裝之後，您就可以在本機執行封裝。  
 
> [!NOTE]
> 在 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 中，已加入新的資料庫角色來支援執行個體層級和資料庫層級的套件安裝權限的範圍設定。 如需詳細資訊，請參閱 [SQL Server 的 R 套件管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。
 

### <a name="location-of-default-r-library-location-for-r-services"></a>R Services 的預設 R 程式庫的位置

如果您已使用預設執行個體安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，執行個體所使用的 R 套件程式庫會位於 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體資料夾中。 例如： 

+ 預設執行個體 _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ 具名執行個體 _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


您可以執行下列陳述式來確認目前的 R 執行個體的預設程式庫。 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

如需詳細資訊，請參閱[判斷 SQL Server 上所安裝的套件](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md)。

## <a name="managing-installed-packages"></a>管理已安裝的套件

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 提供用來安裝及管理 R 套件的新功能，可讓資料庫系統管理員和資料科學家兩者對套件使用情形和安裝，有更充分的自由和控制權。 如需詳細資訊，請參閱 [SQL Server 的 R 套件管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。 

如果您使用 SQL Server 2016 R Services，目前無法使用新的套件管理功能。 同時，您有下列選項可用來判斷 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦上所安裝的套件，請使用其中一個選項︰

+ 如果您有資料夾權限，請檢視預設程式庫。
+ 執行 R 命令的命令來列出 R_SERVICES 程式庫位置中的套件
+ 在執行個體上使用預存程序，如下所示︰
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
 [管理和監視 R 方案](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  

