---
title: 管理 Integration Services 服務 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- services [Integration Services], configuring
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6f6251ac85fe76d775fd84b6463d20532615d28c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375126"
---
# <a name="manage-the-integration-services-service"></a>管理 Integration Services 服務
    
> [!IMPORTANT]  
>  本主題會討論 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務，即用於管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支援此服務能與舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]回溯相容。 從 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]開始，您可以管理 Integration Services 伺服器上的物件，例如封裝。  
  
 當安裝 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]元件時，也會安裝 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務。 根據預設， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務會啟動，而且服務的啟動類型會設為自動。 不過，您也必須安裝 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 才能使用此服務來管理已儲存和執行中的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
> [!NOTE]  
>  您無法連接到的執行個體[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]服務[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]新版[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 也就是說，在 **[連接到伺服器]** 對話方塊中，您無法輸入只有執行 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 版本之 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務的伺服器名稱。 不過，您可以從 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 版本的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 編輯此服務的組態檔，進而管理儲存在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]執行個體中的封裝。 如需詳細資訊，請參閱 [設定 Integration Services 服務 &#40;SSIS 服務&#41;](service/integration-services-service-ssis-service.md)回溯相容。  
  
 您在一部電腦上只能安裝單一 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務的執行個體。 此服務並非特定 [!INCLUDE[ssDE](../includes/ssde-md.md)]執行個體特有的。 您可以使用執行服務所在之電腦的名稱來連接至服務。  
  
 您可以使用下列其中一個 Microsoft Management Console (MMC) 嵌入式管理單元來管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務：SQL Server 組態管理員或服務。 您必須先確定服務已啟動，然後才能管理 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的封裝。  
  
 根據預設，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務設定為可管理 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體之 msdb 資料庫中的封裝，該執行個體與 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 同時安裝。 如果 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體並未同時安裝，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務會設定為可管理本機預設 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體之 msdb 資料庫中的封裝。 若要管理儲存在 [!INCLUDE[ssDE](../includes/ssde-md.md)]具名或遠端執行個體中的封裝，或儲存在多個 [!INCLUDE[ssDE](../includes/ssde-md.md)]執行個體中的封裝，您就必須修改此服務的組態檔。 如需詳細資訊，請參閱 [設定 Integration Services 服務 &#40;SSIS 服務&#41;](service/integration-services-service-ssis-service.md)回溯相容。  
  
 依預設， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務會設定為在服務停止時停止執行中的封裝。 不過， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務不會等待封裝停止，在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務停止後，仍可能有部份封裝在執行中。  
  
 如果 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務已停止，可以使用 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 匯入和匯出精靈]、[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師、執行封裝公用程式及 **dtexec** 命令提示字元公用程式 (dtexec.exe) 繼續執行封裝。 不過，您無法監視執行中的封裝。  
  
 根據預設， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務會在 NETWORK SERVICE 帳戶內容中執行。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務會寫入 Windows 事件記錄檔。 您可以在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中檢視服務事件。 此外，您也可以使用「Windows 事件檢視器」來檢視服務事件。  
  
### <a name="to-set-properties-of-integration-services-service-using-the-services-snap-in"></a>若要使用「服務」嵌入式管理單元設定 Integration Services 服務的屬性  
  
-   [設定 Integration Services 服務的屬性](../../2014/integration-services/set-the-properties-of-the-integration-services-service.md)  
  
### <a name="to-view-service-events-for-integration-services-service"></a>檢視 Integration Services 服務的服務事件  
  
-   [檢視 Integration Services 服務的事件](../../2014/integration-services/view-events-for-the-integration-services-service.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 服務 &#40;SSIS 服務&#41;](service/integration-services-service-ssis-service.md)   
 [設定 Integration Services 服務 &#40;SSIS 服務&#41;](configuring-the-integration-services-service-ssis-service.md)   
 [SQL Server 匯入和匯出精靈](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [dtexec 公用程式](packages/dtexec-utility.md)   
 [執行專案和封裝](packages/run-integration-services-ssis-packages.md)  
  
  
