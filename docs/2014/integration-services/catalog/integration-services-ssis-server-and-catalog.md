---
title: Integration Services (SSIS) 伺服器 |Microsoft 文件
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 69598f8ca412e32a76ea841f9a234d01c6847718
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145442"
---
# <a name="integration-services-ssis-server"></a>Integration Services (SSIS) 伺服器
  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中設計和測試封裝之後，可以將含有那些封裝的專案部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器為主控 `SSISDB` 資料庫之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體。 資料庫會儲存封裝、專案、參數、權限、伺服器屬性與作業歷程記錄等物件。  
  
 `SSISDB` 資料庫會透過可供您查詢的公用檢視，公開物件資訊。 此資料庫也會提供預存程序，讓您可加以呼叫來管理物件。  
  
 在您將專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器之前，必須先建立 `SSISDB` 目錄。  
  
 如需 SSISDB 目錄功能的概觀，請參閱 [SSIS 目錄](ssis-catalog.md)。  
  
## <a name="high-availability"></a>高可用性  
 其他使用者與資料庫一樣， `SSISDB` database 支援資料庫鏡像和複寫。 如需鏡像及複寫的詳細資訊，請參閱[資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
 您也可以使用 SSIS 和 AlwaysOn 可用性群組提供 SSISDB 及其內容的高可用性。 如需詳細資訊，請參閱 blogs.msdn.com 上這篇 Matt Masson 的部落格文章： [SSIS 與 AlwaysOn](http://go.microsoft.com/fwlink/?LinkId=255873)。  
  
##  <a name="ssms"></a> SQL Server Management Studio 中的 Integration Services Server  
 當您連接到主控 `SSISDB` 資料庫的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體時，您會在 [物件總管] 中看到以下物件：  
  
-   **SSISDB 資料庫**  
  
     `SSISDB`資料庫會出現在**資料庫**在 [物件總管] 節點。 您可以查詢檢視，並呼叫管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器和儲存在伺服器上之物件的預存程序。  
  
-   **Integration Services 目錄**  
  
     **[Integration Services 目錄]** 節點下方有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案和環境的資料夾。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [建立 SSIS 目錄](../create-the-ssis-catalog.md)  
  
-   [檢視 Integration Services 伺服器上的套件清單](view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [將專案部署至 Integration Services 伺服器](../deploy-projects-to-integration-services-server.md)  
  
-   [使用 SQL Server Management Studio 在 SSIS 伺服器上執行套件](../run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="related-content"></a>相關內容  
 blogs.msdn.com 上的部落格文章： [SSIS 與 AlwaysOn](http://go.microsoft.com/fwlink/?LinkId=255873)。  
  
  