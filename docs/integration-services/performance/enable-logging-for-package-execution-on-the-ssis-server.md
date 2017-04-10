---
title: "在 SSIS 伺服器上啟用封裝執行的記錄功能 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.SSIS.SSMS.ISMANAGECUSTOMIZEDLOGGINGLEVEL.F1"
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# 在 SSIS 伺服器上啟用封裝執行的記錄功能
  本主題描述如何在執行已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的封裝時，設定或變更封裝的記錄層級。 執行封裝時設定的記錄層級會覆寫您在設計期間於 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中設定的封裝記錄。 如需詳細資訊，請參閱[在 SQL Server Data Tools 中啟用封裝記錄功能](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)。  
  
 在 SQL Server 的 [伺服器屬性] 中，您可以在 [伺服器記錄層級] 屬性下方，選取預設的全伺服器記錄層級。 您可以挑選本主題所說明的其中一個內建記錄層級，或者可挑選現有的自訂記錄層級。 選取的記錄層級預設會套用到所有部署到 SSIS 目錄的封裝。 它預設也會套用到執行 SSIS 封裝的 SQL 代理程式工作步驟。  
  
 您可以使用下列其中一個方法來指定個別封裝的記錄層級。 本主題涵蓋第一個方法。  
  
-   使用執行封裝對話方塊設定封裝執行作業的執行個體  
  
-   請使用 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) 為執行的執行個體設定參數。  
  
-   使用 [新增作業步驟] 對話方塊設定封裝執行作業的 SQL Server Agent 作業。  
  
## 使用執行封裝對話方塊設定封裝的記錄層級  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [物件總管] 中，導覽至封裝。  
  
2.  以滑鼠右鍵按一下封裝，然後選取 [執行]。  
  
3.  在 **[執行封裝]** 對話方塊中，選取 **[進階]** 索引標籤。  
  
4.  在 **[記錄層次]**底下，選取記錄層次。 本主題包含可用值的描述。  
  
5.  完成任何其他封裝組態，然後按一下 **[確定]** 執行封裝。  
  
## 選取記錄層級  
 下面是可用的內建記錄層級。 您也可以選取現有的自訂記錄層級。 本主題包含自訂記錄層級的描述。  
  
|[記錄層次]|說明|  
|-------------------|-----------------|  
|無|關閉記錄功能。 只記錄封裝執行狀態。|  
|Basic|記錄所有事件，自訂和診斷事件除外。 這是預設值。|  
|RuntimeLineage|收集追蹤資料流程中歷程資訊所需的資料。 您可以剖析此歷程資訊，以對應工作間的歷程關聯性。 ISV 和開發人員可以使用此資訊來建置自訂歷程對應工具。|  
|效能|只記錄效能統計資料，以及 OnError 和 OnWarning 事件。<br /><br /> **[執行效能]** 報表會顯示封裝資料流程元件的 [啟用時間] 和 [總時間]。 最後一個封裝執行作業的記錄層次設定為 **[效能]** 或 **[詳細資訊]**時，就可使用這項資訊。 如需詳細資訊，請參閱 [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md)。<br /><br /> [catalog.execution_component_phases](../../integration-services/system-views/catalog-execution-component-phases.md) 檢視會顯示每一個執行階段之資料流程元件的開始和結束時間。 此檢視只會在封裝執行作業的記錄層次設定為 **[效能]** 或 **[詳細資訊]**時，顯示這些元件的這項資訊。|  
|[詳細資訊]|記錄所有事件，包括自訂和診斷事件。<br /><br /> 自訂事件包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 工作所記錄的事件。 如需有關自訂事件的詳細資訊，請參閱 [Custom Messages for Logging](../../integration-services/performance/custom-messages-for-logging.md)。<br /><br /> **DiagnosticEx** 事件即為診斷事件的範例。 每當「執行封裝」工作執行子封裝時，此事件就會擷取傳遞至子封裝的參數值。<br /><br /> **DiagnosticEx** 事件也可協助您取得發生資料列層級錯誤的資料行名稱。 此事件會將資料流程歷程對應寫入記錄檔。 您接著可以使用錯誤輸出所擷取的資料行識別碼，在此歷程對應中查詢資料行名稱。  如需詳細資訊，請參閱＜ [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md)＞。<br /><br /> **DiagnosticEx** 的訊息資料行值是 XML 文字。 若要檢視封裝執行的訊息文字，請查詢 [catalog.operation_messages &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) 檢視。 請注意， **DiagnosticEx** 事件不會在其 XML 輸出中保留空白，以縮減記錄檔的大小。 若要改善可讀性，可將記錄檔複製到 XML 編輯器 (例如，在 Visual Studio 中)，該編輯器需支援 XML 格式設定和語法反白顯示。<br /><br /> 每當資料流程元件傳送資料至封裝執行的下游元件，[catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) 檢視就會顯示一個資料列。 您必須將記錄層次設定為 **[詳細資訊]** ，以擷取檢視中的這項資訊。|  
  
## 使用自訂的記錄層級管理對話方塊建立和管理自訂的記錄層級  
 您可以建立自訂的記錄層級，只收集您所需的統計資料和事件。 您也可以選擇性擷取事件的內容，包括變數值、連接字串及元件屬性。 當您執行封裝時，每當您可以選取內建記錄層級時，就能選取自訂的記錄層級。  
  
> [!TIP]  
>  若要擷取封裝變數的值，變數的 **IncludeInDebugDump** 屬性必須設定為 [True]。  
  
1.  若要建立和管理自訂的記錄層級，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下 SSISDB 資料庫，然後選取 [自訂的記錄層級] 以開啟 [自訂記錄層級管理] 對話方塊。 [自訂的記錄層級]  清單包含所有現有的自訂記錄層級。  
  
2.  若要 **建立** 新的自訂記錄層級，可按一下 [建立] ，然後提供名稱和描述。 在 [統計資料]  和 [事件]  索引標籤上，選擇您想要收集的統計資料與事件。 在 [事件]  索引標籤上，選擇性地選取個別事件的 [包含內容]  。 然後按一下 [儲存] 。  
  
3.  若要 **更新** 現有的自訂記錄層級，可在清單中選取該層級、重新進行設定，然後按一下 [儲存] 。  
  
4.  若要 **刪除** 現有的自訂記錄層級，可在清單中選取該層級，然後按一下 [刪除] 。  
  
 **自訂記錄層級的權限。**  
  
-   SSISDB 資料庫的所有使用者都能看見自訂的記錄層級，並在執行封裝時，選取自訂的記錄層級。  
  
-   只有 ssis_admin 或 sysadmin 角色的使用者，才可以建立、 更新或刪除自訂的記錄層級。  
  
## 請參閱＜  
 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)   
 [在 SQL Server Data Tools 中啟用封裝記錄功能](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)  
  
  