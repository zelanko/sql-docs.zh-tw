---
title: 檢視及停止封裝執行整合服務的伺服器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing running packages [Integration Services]
- packages [Integration Services], running
- running package [Integration Services], managing
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
caps.latest.revision: 17
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cef267dbb770c0ccb39ea40143ce9591f915db5c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37215828"
---
# <a name="viewing-and-stopping-packages-running-on-the-integration-services-server"></a>檢視及停止在 Integration Services 伺服器上執行的封裝
  `SSISDB`資料庫不會對使用者顯示的內部資料表中儲存執行歷程記錄。 不過，它會透過可供您查詢的公用檢視來公開您需要的資訊。 另外，它也會提供預存程序，讓您可以加以呼叫，以執行與封裝相關的一般工作。  
  
 通常，您會在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中管理伺服器上的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]物件。 但您也可以直接查詢資料庫檢視並呼叫預存程序，或編寫可呼叫 Managed API 的自訂程式碼。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 和 managed 的 API 會查詢檢視並呼叫預存程序，來執行其多數工作。 例如，您可以檢視目前正在伺服器上執行之 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的清單，並在需要時要求停止封裝。  
  
## <a name="viewing-the-list-of-running-packages"></a>檢視執行中封裝的清單  
 您可以在 **[作用中的作業]** 對話方塊中檢視目前正在伺服器上執行之封裝的清單。 如需詳細資訊，請參閱 [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md)。  
  
 如需有關可用來檢視執行中封裝清單之其他方法的詳細資訊，請參閱下列主題。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 存取  
 若要檢視正在伺服器上執行之封裝的清單，請針對狀態 2 的封裝查詢檢視 [catalog.executions &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database) 。  
  
 透過 Managed API 來以設計程式方式存取  
 請參閱 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間和其類別。  
  
## <a name="stopping-a-running-package"></a>停止執行中的封裝  
 您可以在 **[作用中的作業]** 對話方塊中要求執行中的封裝停止。 如需詳細資訊，請參閱 [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md)。  
  
 如需有關可用來停止執行中封裝之其他方法的詳細資訊，請參閱下列主題。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 存取  
 若要停止正在伺服器上執行的封裝，請呼叫預存程序 [catalog.stop_operation &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database)。  
  
 透過 Managed API 來以設計程式方式存取  
 請參閱 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間和其類別。  
  
## <a name="viewing-the-history-of-packages-that-have-run"></a>檢視已執行封裝的記錄  
 若要檢視已在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]中執行之封裝的記錄，請使用 **[所有執行]** 報表。 如需 [所有執行] 報表和其他標準報表的詳細資訊，請參閱 [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md) (Integration Services 伺服器的報表)。  
  
 如需有關可用來檢視執行中封裝記錄之其他方法的詳細資訊，請參閱下列主題。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 存取  
 若要檢視已執行封裝的資訊，請查詢檢視 [catalog.executions &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)。  
  
 透過 Managed API 來以設計程式方式存取  
 請參閱 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間和其類別。  
  
## <a name="see-also"></a>另請參閱  
 [執行專案和套件](packages/run-integration-services-ssis-packages.md)   
 [套件執行的疑難排解報告](troubleshooting/troubleshooting-reports-for-package-execution.md)  
  
  
