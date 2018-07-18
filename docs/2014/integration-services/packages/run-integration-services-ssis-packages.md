---
title: 執行專案和套件 |Microsoft Docs
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
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cc9e292b67bd282351bdea60068a58a39ecb0aad
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287604"
---
# <a name="execution-of-projects-and-packages"></a>執行專案和封裝
  若要執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，您可以根據這些封裝的儲存位置使用數種工具的其中一種。 工具會列在下表中。  
  
 若要將封裝儲存於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器，您可使用專案部署模型將專案部署到伺服器上。 如需相關資訊，請參閱 [將專案部署至 Integration Services 伺服器](../deploy-projects-to-integration-services-server.md)。  
  
 若要將封裝儲存在 SSIS 封裝存放區、msdb 資料庫或是檔案系統中，您可使用封裝部署模型。 如需詳細資訊，請參閱 <<c0> [ 封裝部署&#40;SSIS&#41;](legacy-package-deployment-ssis.md)。</c0>  
  
|工具|儲存在 Integration Services 伺服器上的封裝|儲存在 SSIS 封裝存放區或是 msdb 資料庫中的封裝|儲存在檔案系統中，但不在 SSIS 封裝存放區中的封裝|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|否|否<br /><br /> 但是，您可以將 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區中現有的封裝加入專案，其中包括 msdb 資料庫。 用這種方式來將現有封裝加入專案，會在檔案系統中建立封裝的本機複本。|是|  
|**SQL Server Management Studio (當您連接到主控 Integration Services 伺服器的 Database Engine 執行個體時)**<br /><br /> 如需詳細資訊，請參閱 [執行封裝對話方塊](../execute-package-dialog-box.md)|是|否<br /><br /> 但是，您可以將封裝從這些位置匯入伺服器。|否<br /><br /> 但是，您可以將封裝從檔案系統匯入伺服器。|  
|**SQL Server Management Studio (當連接到管理 SSIS 套件存放區的 Integration Services 服務時)**|否|是|否<br /><br /> 但是，您可以從檔案系統將封裝匯入 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區。|  
|**dtexec**<br /><br /> 如需詳細資訊，請參閱 [dtexec Utility](dtexec-utility.md)。|是|是|是|  
|**dtexecui**<br /><br /> 如需詳細資訊，請參閱[執行封裝公用程式 &#40;DtExecUI&#41; UI 參考](execute-package-utility-dtexecui-ui-reference.md)|否|是|是|  
|**SQL Server Agent**<br /><br /> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業排程封裝。<br /><br /> 如需詳細資訊，請參閱 [封裝的 SQL Server Agent 作業](sql-server-agent-jobs-for-packages.md)。|是|是|是|  
|**內建預存程序**<br /><br /> 如需詳細資訊，請參閱 [catalog.start_execution &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)|是|否|否|  
|**Managed API (使用** <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間中的類型和成員)|是|否|否|  
|**Managed API (使用** <xref:Microsoft.SqlServer.Dts.Runtime> 命名空間中的類型和成員)|非目前|是|是|  
  
## <a name="execution-and-logging"></a>執行與記錄  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝可以啟用記錄功能，您可以在記錄檔中擷取執行階段資訊。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)。  
  
 您可以使用作業報表監視部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器並在其中執行的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中可提供此報告。 如需詳細資訊，請參閱 [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用 SQL Server Agent 排程套件](../schedule-a-package-by-using-sql-server-agent.md)  
  
-   [在 SQL Server Data Tools 中執行套件](../run-a-package-in-sql-server-data-tools.md)  
  
-   [使用 SQL Server Management Studio 在 SSIS 伺服器上執行套件](../run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另請參閱  
 [dtexec 公用程式](dtexec-utility.md)   
 [SQL Server 匯入和匯出精靈](../import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)  
  
  
