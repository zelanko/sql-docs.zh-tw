---
title: 以程式設計方式執行及管理套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: run-manage-packages-programmatically
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 1a08c75e-ce8c-45ee-81bd-32248bbdb2b2
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 354f7f276cd99ce78f89d48e0651b46be997d33c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="running-and-managing-packages-programmatically"></a>以程式設計方式執行及管理封裝
  如果您需要在開發環境以外的地方管理和執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，可以使用程式設計方式操作封裝。 在這種方法中，您有許多的選擇：  
  
-   在不須修改的情況下載入並執行現有的封裝。  
  
-   載入現有的封裝、重新設定 (例如，針對不同的資料來源) 然後加以執行。  
  
-   建立新封裝、逐物件和逐屬性地加入與設定元件、儲存，然後加以執行。  
  
 您可以只撰寫幾行程式碼，從用戶端應用程式載入及執行現有的封裝。  
  
 本章節描述及示範如何以程式設計方式執行現有的封裝，以及如何從其他應用程式存取資料流程的輸出。 如同進階程式設計選項，您能夠以程式設計方式逐行建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件 (如[以程式設計方式建置套件](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)主題中所述)。  
  
 本章節也會討論您可以使用程式設計方式執行的其他管理工作，以管理預存程序、執行中的封裝和封裝角色。  
  
## <a name="running-packages-on-the-integration-services-server"></a>在 Integration Services 伺服器上執行封裝  
 當您將封裝部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器時，可以使用 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間，以程式設計方式執行封裝。 Microsoft.SqlServer.Management.IntegrationServices 組件是使用 .NET Framework 3.5 編譯的。 如果您要建置 .NET Framework 4.0 應用程式，可能需要將組件參考直接加入至專案檔案。  
  
 您也可以使用此命名空間，在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上部署和管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。 如需命名空間的概觀和程式碼片段，請參閱 blogs.msdn.com 上的部落格文章：[SSIS 目錄管理物件模型初探](http://go.microsoft.com/fwlink/?LinkId=253122)。  
  
## <a name="in-this-section"></a>本節內容  
 [了解本機和遠端執行之間的差異](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)  
 討論在本機執行封裝以及在伺服器上執行封裝之間的重大差異。  
  
 [以程式設計方式載入和執行本機套件](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
 描述如何在本機電腦上從用戶端應用程式執行現有的封裝。  
  
 [以程式設計方式載入和執行遠端套件](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
 描述如何從用戶端應用程式執行現有的封裝，並確保此封裝是在伺服器上執行。  
  
 [載入本機套件的輸出](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
 描述如何使用 DataReader 目的地和 DtsClient 命名空間在本機電腦上執行封裝，以及如何將資料流程輸出載入用戶端應用程式內。  
  
 [以程式設計方式列舉可用的套件](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
 描述如何探索受到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務所管理的可用封裝。  
  
 [以程式設計方式管理套件與資料夾](../../integration-services/run-manage-packages-programmatically/managing-packages-and-folders-programmatically.md)  
 描述如何建立、重新命名及刪除封裝和資料夾。  
  
 [以程式設計方式管理執行中的套件](../../integration-services/run-manage-packages-programmatically/managing-running-packages-programmatically.md)  
 描述如何列出目前正在執行的封裝、檢查封裝的屬性，並停止執行中的封裝。  
  
 [以程式設計方式管理套件角色 &#40;SSIS 服務&#41;](../../integration-services/run-manage-packages-programmatically/managing-package-roles-programmatically-ssis-service.md)  
 描述如何取得或設定指派給封裝或資料夾之角色的相關資訊。  
  
## <a name="reference"></a>參考  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)  
 列出預先定義的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤碼，以及其符號名稱與描述。  
  
## <a name="related-sections"></a>相關章節  
 [使用指令碼擴充套件](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 討論如何透過使用指令碼工作擴充控制流程，或是如何透過使用指令碼元件擴充資料流程。  
  
 [使用自訂物件擴充封裝](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 討論如何建立程式自訂工作、資料流程元件以及其他封裝物件，以供在多個封裝中使用。  
  
 [以程式設計方式建置套件](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 討論如何以程式設計方式建立、設定和儲存 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
