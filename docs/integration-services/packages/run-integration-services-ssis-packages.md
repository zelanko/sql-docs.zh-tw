---
title: "執行 Integration Services (SSIS) 封裝 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 封裝, 執行"
  - "SSIS 封裝, 執行"
  - "封裝 [Integration Services]，執行"
  - "SQL Server Integration Services 封裝, 執行"
  - "執行封裝 [Integration Services]"
  - "執行封裝 [Integration Services]"
  - "Integration Services, (請參閱 Integration Services 封裝)"
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
caps.latest.revision: 65
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# 執行 Integration Services (SSIS) 封裝
  若要執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，您可以根據這些封裝的儲存位置使用數種工具的其中一種。 工具會列在下表中。  
  
 若要將封裝儲存於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器，您可使用專案部署模型將專案部署到伺服器上。 如需相關資訊，請參閱 [將專案部署至 Integration Services 伺服器](../../integration-services/packages/deploy-projects-to-integration-services-server.md)。  
  
 若要將封裝儲存在 SSIS 封裝存放區、msdb 資料庫或是檔案系統中，您可使用封裝部署模型。 如需詳細資訊，請參閱[舊版封裝部署 &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)。  
  
|工具|儲存在 Integration Services 伺服器上的封裝|儲存在 SSIS 封裝存放區或是 msdb 資料庫中的封裝|儲存在檔案系統中，但不在 SSIS 封裝存放區中的封裝|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|否|否<br /><br /> 但是，您可以將 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區中現有的封裝加入專案，其中包括 msdb 資料庫。 用這種方式來將現有封裝加入專案，會在檔案系統中建立封裝的本機複本。|是|  
|**SQL Server Management Studio (當您連接到主控 Integration Services 伺服器的 Database Engine 執行個體時)**<br /><br /> 如需詳細資訊，請參閱 [執行封裝對話方塊](../../integration-services/packages/execute-package-dialog-box.md)|是|否<br /><br /> 但是，您可以將封裝從這些位置匯入伺服器。|否<br /><br /> 但是，您可以將封裝從檔案系統匯入伺服器。|
|**SQL Server Management Studio (當您連接到主控已啟用為相應放大主機之 Integration Services 伺服器的 Database Engine 執行個體時)**<br /><br /> 如需詳細資訊，請參閱[在 [相應放大] 中執行套件](../Topic/Run%20Packages%20in%20Integration%20Services%20\(SSIS\)%20Scale%20Out.md)|是|否|否|
|**SQL Server Management Studio (當連接到管理 SSIS 套件存放區的 Integration Services 服務時)**|否|是|否<br /><br /> 但是，您可以從檔案系統將封裝匯入 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區。|  
|**dtexec**<br /><br /> 如需詳細資訊，請參閱 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)。|是|是|是|  
|**dtexecui**<br /><br /> 如需詳細資訊，請參閱[執行封裝公用程式 &#40;DtExecUI&#41; UI 參考](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)|否|是|是|  
|**SQL Server Agent**<br /><br /> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業排程封裝。<br /><br /> 如需詳細資訊，請參閱 [封裝的 SQL Server Agent 作業](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)。|是|是|是|  
|**內建預存程序**<br /><br /> 如需詳細資訊，請參閱 [catalog.start_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)|是|否|否|  
|**Managed API (使用** <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間中的類型和成員)|是|否|否|  
|**Managed API (使用 **<xref:Microsoft.SqlServer.Dts.Runtime> 命名空間中的類型和成員)|非目前|是|是|  
  
## <a name="execution-and-logging"></a>執行與記錄  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝可以啟用記錄功能，您可以在記錄檔中擷取執行階段資訊。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
 您可以使用作業報表監視部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器並在其中執行的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中可提供此報告。 如需詳細資訊，請參閱 [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用 SQL Server Agent 排程套件](../../integration-services/packages/schedule-a-package-by-using-sql-server-agent.md)  
  
-   [在 SQL Server Data Tools 中執行套件](../../integration-services/packages/run-a-package-in-sql-server-data-tools.md)  
  
-   [使用 SQL Server Management Studio 在 SSIS 伺服器上執行套件](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另請參閱  
 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)   
[啟動 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  