---
title: "建立使用本機封裝儲存機制的 miniCRAN | Microsoft Docs"
ms.custom: ""
ms.date: "05/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 4
---
# 建立使用本機封裝儲存機制的 miniCRAN
本主題說明如何建立使用 R 封裝的本機 R 封裝儲存機制 **miniCRAN**。 

因為 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體通常位於伺服器上沒有網際網路連線，安裝 R 封裝的標準方法 (R 命令 `install.packages()`) 可能無法運作，因為套件安裝程式無法存取或稱為 CRAN 或是任何其他鏡像站台。

有兩個選項，從本機共用或儲存機制安裝封裝︰

+ 若要建立的封裝，您需要然後再從這個儲存機制安裝的本機儲存機制使用 miniCRAN 封裝。 本主題說明 miniCRAN 方法。

+ 下載您需要套件和它們的相依性為 zip 檔案，並將它們儲存在本機資料夾，然後將複製到該資料夾 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦。 如需有關手動複製方法的詳細資訊，請參閱 [安裝 SQL Server 上的其他封裝](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)。


## 步驟 1： 安裝 miniCRAN 並下載的封裝 


1. 可以存取網際網路的電腦上安裝 miniCRAN 封裝。

   ~~~~
   # Install miniCRAN ---------------------------------------------------

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. 下載或安裝到這台電腦需要的封裝。 這會建立您要複製之封裝的資料夾結構 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 更新版本。

   ~~~~
   # List the packages you need 
   # Do not specify dependencies
   pkgs_needed <- c("ggplot2", "ggdendro")
   ~~~~

3. 複製到 R_SERVICES 程式庫的 miniCRAN 儲存機制上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體。

## 步驟 2： SQL Server 電腦上安裝封裝 

4. 在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行 R 命令的電腦  `install.packages()`。 您可以使用其中一種隨 R 工具 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], ，例如 Rgui.exe，或者您可以執行命令的一部分 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 預存程序。
5. 在提示來指定儲存機制中，選取包含您剛才複製; 檔案的資料夾亦即，本機 miniCRAN 儲存機制。

   ~~~~
   pkgs_needed <- c("ggplot2", "ggdendro")
   local_repo  <- "~/miniCRAN"
   
   .libPaths()[1]
   "C:/Program Files/Microsoft SQL Server/130/R_SERVER/library"

   lib <- .libPaths()[1]

   install.packages(pkgs_needed, 
                 repos = file.path("file://", normalizePath(local_repo, winslash = "/")),
                 lib = lib,
                 type = "win.binary",
                 dependencies = TRUE
                 )
   ~~~~

6. 請確認封裝已安裝執行此 R 程式碼。
   ~~~~
   installed.packages()
   ~~~~



## 通知

這項資訊的來源是由也開發 miniCRAN 封裝 Andre de Vries 這篇文章。 詳細資料及完整的逐步解說，請參閱  [離線的 SQL Server 2016 執行個體中的封裝如何安裝 R](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)