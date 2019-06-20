---
title: 啟用記錄 for Package Execution on the SSIS Server |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47f74d4510b46b984eb58706ff4ac159cb8b1352
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059366"
---
# <a name="enable-logging-for-package-execution-on-the-ssis-server"></a>在 SSIS 伺服器上啟用封裝執行的記錄功能
  此程序描述如何在執行已經部署至 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器的封裝時，設定或變更封裝的記錄層次。 執行封裝時所設定的記錄層次會覆寫您使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 設定的封裝記錄。 如需詳細資訊，請參閱 [在 SQL Server Data Tools 中啟用封裝記錄功能](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md) 。  
  
 您可以使用下列其中一個方法指定記錄層次： 本主題涵蓋第一個方法。  
  
-   使用執行封裝對話方塊設定封裝執行作業的執行個體  
  
-   請使用 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) 為執行的執行個體設定參數。  
  
-   使用 [新增作業步驟] 對話方塊設定封裝執行作業的 SQL Server Agent 作業。  
  
### <a name="to-set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>若要使用執行封裝對話方塊設定封裝的記錄層次  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的 [物件總管] 中，導覽至封裝。  
  
2.  以滑鼠右鍵按一下封裝，然後選取 [執行]。  
  
3.  在 **[執行封裝]** 對話方塊中，選取 **[進階]** 索引標籤。  
  
4.  在 **[記錄層次]** 底下，選取記錄層次。 如需可用值的說明，請參閱下表。  
  
5.  完成任何其他封裝組態，然後按一下 **[確定]** 執行封裝。  
  
 下面是可用的記錄層次。  
  
|[記錄層次]|描述|  
|-------------------|-----------------|  
|None|關閉記錄功能。 只記錄封裝執行狀態。|  
|[基本]|記錄所有事件，自訂和診斷事件除外。 這是預設值。|  
|效能|只記錄效能統計資料，以及 OnError 和 OnWarning 事件。<br /><br /> **[執行效能]** 報表會顯示封裝資料流程元件的 [啟用時間] 和 [總時間]。 最後一個封裝執行作業的記錄層次設定為 **[效能]** 或 **[詳細資訊]** 時，就可使用這項資訊。 如需詳細資訊，請參閱 [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md)。<br /><br /> [catalog.execution_component_phases](/sql/integration-services/system-views/catalog-execution-component-phases) 檢視會顯示每一個執行階段之資料流程元件的開始和結束時間。 此檢視只會在封裝執行作業的記錄層次設定為 **[效能]** 或 **[詳細資訊]** 時，顯示這些元件的這項資訊。|  
|「詳細資訊」|記錄所有事件，包括自訂和診斷事件。<br /><br /> DiagnosticEx 事件即為診斷事件的範例。 只要執行封裝工作執行子封裝，它就會記錄這個事件。 事件訊息是由傳遞至子封裝的參數值所組成。<br /><br /> DiagnosticEx 之訊息資料行的值是 XML 文字。 . 若要檢視封裝執行的訊息文字，請查詢 [catalog.operation_messages &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database) 檢視。<br /><br /> 注意:自訂事件包括 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 工作所記錄的事件。 如需詳細資訊，請參閱 [自訂訊息以進行記錄](../../2014/integration-services/custom-messages-for-logging.md)。<br /><br /> 每當資料流程元件傳送資料至封裝執行的下游元件， [catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) 檢視就會顯示一個資料列。 您必須將記錄層次設定為 **[詳細資訊]** ，以擷取檢視中的這項資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 記錄](performance/integration-services-ssis-logging.md)   
 [在 SQL Server Data Tools 中啟用封裝記錄功能](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)  
  
  
