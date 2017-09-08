---
title: "使用 miniCRAN 來建立本機套件儲存機制 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8af93b3e132290eef4b43da568b9381ff8e5a04
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-local-package-repository-using-minicran"></a>使用 miniCRAN 來建立本機套件儲存機制
本主題說明如何使用 R 套件 **miniCRAN** 來建立本機 R 套件儲存機制。 

由於 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體通常位於無法連線到網際網路的伺服器上，因此標準的 R 套件安裝方式 (R 命令 `install.packages()`) 可能無法運作，因為套件安裝程式無法存取 CRAN 或任何其他鏡像站台。

有兩個選項可從本機共用或儲存機制安裝套件：

+ 使用 miniCRAN 套件來建立您所需套件的本機儲存機制，然後從這個儲存機制安裝。 本主題將說明 miniCRAN 方法。

+ 將您所需的套件及其相依項目下載成 ZIP 檔，並將它們儲存在本機資料夾中，然後將該資料夾複製到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦。 如需有關手動複製方法的詳細資訊，請參閱[在 SQL Server 上安裝其他的 R 套件](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)。


## <a name="step-1-install-minicran-and-download-packages"></a>步驟 1： 安裝 miniCRAN 並下載套件 


1. 在能夠存取網際網路的電腦上安裝 miniCRAN 套件。

   ~~~~
   # Install miniCRAN and igraph

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. 使用下列 R 指令碼將您所需的套件下載或安裝到這部電腦。 這會建立您稍後將套件複製到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 時所需的資料夾結構。

   ~~~~
   # List the packages to get. Do not specify dependencies.
   pkgs_needed <- c("ggplot2", "ggdendro")
   # Plot the dependency graph 
   plot(makeDepGraph(pkgs_needed)) 
   
   # Create the local repo 
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror) 
   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.2") 

   # List local packages 
   pdb <- as.data.frame( 
     pkgAvail(local_repo, type = "win.binary", Rversion = "3.2"),  
     stringsAsFactors = FALSE) 
   head(pdb) 
   pdb$Package 
   pdb[, c("Package", "Version", "License")] 
   ~~~~


## <a name="step-2-copy-the-minicran-repository-to-the-sql-server-computer"></a>步驟 2： 將 miniCRAN 儲存機制複製到 SQL Server 電腦 

將 miniCRAN 儲存機制複製到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體上的 R_SERVICES 程式庫。

+ 就 SQL Server 2016 而言，預設資料夾是 `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library1`。
+ 預設資料夾是針對 SQL Server 2017， `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library1`。

如果您已使用具名的執行個體來安裝 R Services，請務必在路徑中包含執行個體名稱，以確保將程式庫安裝到正確的執行個體。 例如，如果您的具名執行個體是 RTEST02，則具名執行個體的預設路徑將會是：`C:\Program Files\Microsoft SQL Server\MSSQL13.RTEST02\R_SERVICES\library`。

如果您已將 SQL Server 安裝到不同的磁碟機，或在安裝路徑中進行了任何其他變更，並務必一併進行這些變更。

## <a name="step-3-install-the-packages-on-sql-server-using-the-minicran-repository"></a>步驟 3： 使用 miniCRAN 儲存機制在 SQL Server 上安裝套件

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦上，以系統管理員身分開啟 R 命令行或 RGUI。 
  
> [!TIP]
> 您可能在電腦上有多個 R 程式庫；因此，為了確保將套件安裝到正確的執行個體，請使用與您想要安裝套件的特定執行個體一起安裝的 RGUI 或 RTerm 複本。
  
當提示您指定儲存機制時，請選取包含您剛複製之檔案的資料夾；也就是本機 miniCRAN 儲存機制。

   ~~~~
   # Run this R code as administrator on the SQL Server computer 
   pkgs_needed <- c("ggplot2", "ggdendro") 
   local_repo  <- "~/miniCRAN" 

   # OPTIONAL: If you are not running R from the instance library as recommended, you must specify the path
   #   .libPaths()[1] 
   # "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library " 
   # lib <- .libPaths()[1]
   
   install.packages(pkgs_needed,  
                    repos = file.path("file://", normalizePath(local_repo, winslash = "/")), 
                    lib = lib, 
                    type = "win.binary", 
                    dependencies = TRUE 
                    ) 
   installed.packages() 
   ~~~~

確認已安裝套件。
   ~~~~
   installed.packages()
   ~~~~



## <a name="acknowledgements"></a>通知

這項資訊的來源是 Andre de Vries 所撰寫的這篇文章，他也是 miniCRAN 套件的開發者。 如需詳細資料和完整的逐步解說，請參閱[如何在離線的 SQL Server 2016 執行個體上安裝 R 套件 (英文)](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)

