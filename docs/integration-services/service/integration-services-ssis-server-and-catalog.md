---
title: "Integration Services (SSIS) 伺服器和目錄 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "封裝 [Integration Services]，管理"
  - "管理封裝 [Integration Services]"
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Integration Services (SSIS) 伺服器和目錄
  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中設計和測試封裝之後，可以將含有那些封裝的專案部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器是執行個體 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 裝載 **SSISDB** 資料庫。 資料庫會儲存封裝、專案、參數、權限、伺服器屬性與作業歷程記錄等物件。  
  
 **SSISDB** 資料庫會透過可供您查詢的公用檢視，公開物件資訊。 此資料庫也會提供預存程序，讓您可加以呼叫來管理物件。  
  
 您可以部署專案之前 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器，您必須建立 **SSISDB** 類別目錄。  
  
 如需 SSISDB 目錄功能的概觀，請參閱 [SSIS 目錄](../../integration-services/service/ssis-catalog.md)。  
  
## 高可用性  
 與其他使用者資料庫一樣， **SSISDB** 資料庫也支援資料庫鏡像和複寫。 如需有關鏡像和複寫的詳細資訊，請參閱 [資料庫鏡像 & #40。SQL Server & #41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
 您也可以藉由提供 SSISDB 及其內容的高可用性使用 SSIS 和 Alwayson 可用性群組。 如需詳細資訊，請參閱此篇部落格文章 Matt Masson [SSIS 與 Alwayson](http://go.microsoft.com/fwlink/?LinkId=255873), ，在 blogs.msdn.com。  
  
##  <a name="ssms"></a> SQL Server Management Studio 中的 Integration Services Server  
 當您連接到的執行個體 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 裝載 **SSISDB** 資料庫，您會看到物件總管] 中的下列物件︰  
  
-   **SSISDB 資料庫**  
  
     **SSISDB** 資料庫會出現在 [物件總管] 的 **[資料庫]** 節點下方。 您可以查詢檢視，並呼叫管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器和儲存在伺服器上之物件的預存程序。  
  
-   **Integration Services 目錄**  
  
     **[Integration Services 目錄]** 節點下方有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案和環境的資料夾。  
  
## 相關工作  
  
-   [建立 SSIS 目錄](../../integration-services/service/create-the-ssis-catalog.md)  
  
-   [檢視 Integration Services 伺服器上的封裝清單](../../integration-services/service/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [將專案部署至 Integration Services 伺服器](../../integration-services/packages/deploy-projects-to-integration-services-server.md)  
  
-   [使用 SQL Server Management Studio 在 SSIS 伺服器上執行封裝](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## 相關內容  
 部落格文章 [SSIS 與 Alwayson](http://go.microsoft.com/fwlink/?LinkId=255873), ，在 blogs.msdn.com。  
  
  