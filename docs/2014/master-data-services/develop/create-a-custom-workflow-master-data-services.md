---
title: 建立自訂工作流程 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 8e4403e9-595c-4b6b-9d0c-f6ae1b2bc99d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 73c9371d28e64e41f7e0f7d2a53e94309fc66c28
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469083"
---
# <a name="create-a-custom-workflow-master-data-services"></a>建立自訂工作流程 (Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 使用商務規則建立基本工作流程解決方案，以便根據您所指定的條件，自動更新與驗證資料，並傳送電子郵件通知。 當您需要做的處理比內建工作流程動作所提供的處理還要複雜時，請使用自訂工作流程。 自訂工作流程是您所建立的 .NET 組件。 呼叫您的工作流程組件時，程式碼會採取您的情況所需的任何動作。 例如，如果您的工作流程需要自訂的事件處理 (例如多層審核或複雜決策樹)，可以設定 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 啟動一個自訂工作流程，這個工作流程會分析資料並決定將該資料傳送至何處以待審核。  
  
## <a name="how-custom-workflows-are-processed"></a>如何處理自訂工作流程  
 與處理自訂工作流程有關的主要元件有三個：[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式、SQL Server MDS 工作流程整合服務，以及工作流程處理常式組件。 這些元件處理自訂工作流程的方式如下：  
  
1.  您要使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 驗證啟動工作流程的實體。  
  
2.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 會將符合商務規則條件的成員傳送至 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫中的 Service Broker 佇列。  
  
3.  SQL Server MDS 工作流程整合服務會定期呼叫 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫中的預存程序。  
  
4.  當此預存程序在 Service Broker 佇列中找到記錄時，會將其傳回 SQL Server MDS 工作流程整合服務。  
  
5.  SQL Server MDS 工作流程整合服務會將資料路由傳送至您的工作流程處理常式組件。  
  
> [!NOTE]  
>  注意：SQL Server MDS 工作流程整合服務是要觸發單一處理序。 如果您的自訂程式碼需要複雜處理，請在個別的執行緒中，或在工作流程處理序外部，完成您的處理。  
  
## <a name="configure-master-data-services-for-custom-workflows"></a>設定自訂工作流程的 Master Data Services  
 建立自訂工作流程需要撰寫特定的自訂程式碼，並設定 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 將工作流程資料傳遞至您的工作流程處理常式。 遵循以下步驟啟用自訂工作流程處理：  
  
1.  建立[MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender](/previous-versions/sql/sql-server-2016/hh758785(v=sql.130))的 .net 元件。  
  
2.  設定 SQL Server MDS 工作流程整合服務連線至您的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫，並讓某個標記與您的工作流程處理常式產生關聯。  
  
3.  啟動 SQL Server MDS 工作流程整合服務。  
  
4.  在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中，建立一個啟動工作流程的商務規則，此工作流程會以您工作流程處理常式的名稱標記。  
  
5.  將商務規則套用至觸發您自訂工作流程的成員。  
  
### <a name="create-the-workflow-handler-assembly"></a>建立工作流程處理常式組件  
 自訂工作流程是一個 .NET 類別庫元件，它會實[MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender](/previous-versions/sql/sql-server-2016/hh758785(v=sql.130))介面。 SQL Server MDS 工作流程整合服務會呼叫[MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130))方法來執行您的程式碼。 如需執行[IWorkflowTypeExtender StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130))的範例程式碼，請參閱[自訂工作流程範例 &#40;Master Data Services&#41;](create-a-custom-workflow-example.md)。  
  
 請遵循以下步驟，使用 Visual Studio 2010 建立 SQL Server MDS 工作流程整合服務可以呼叫的組件，以處理自訂工作流程：  
  
1.  在 Visual Studio 2010 中，建立一個使用所選語言的新 [類別庫]**** 專案。 若要建立 C# 類別庫，請選取 [Visual C#\Windows]**** 專案類型，然後選取 [類別庫]**** 範本。 輸入您專案的名稱 (例如 **MDSWorkflowTest**)，然後按一下 [確定]****。  
  
2.  加入 Microsoft.MasterDataServices.WorkflowTypeExtender.dll 的參考。 此元件可以在 \<Your installation folder> \Master 資料 services\webapplication\bin 中找到。  
  
3.  將 'using Microsoft.MasterDataServices.Core.Workflow;' 新增至您的 C# 程式碼檔案。  
  
4.  繼承自您的類別宣告中的[MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender](/previous-versions/sql/sql-server-2016/hh758785(v=sql.130)) 。 類別宣告應該類似：'public class WorkflowTester : IWorkflowTypeExtender'。  
  
5.  執行[MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender](/previous-versions/sql/sql-server-2016/hh758785(v=sql.130))介面。 SQL Server MDS 工作流程整合服務會呼叫[MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130))方法來啟動您的工作流程。  
  
6.  將您的元件複製到 \<Your installation folder> \Master 資料 services\webapplication\bin 中名為 Microsoft.MasterDataServices.Workflow.exe 之 SQL SERVER MDS 工作流程整合服務可執行檔的位置  
  
### <a name="configure-sql-server-mds-workflow-integration-service"></a>設定 SQL Server MDS 工作流程整合服務  
 遵循以下步驟，編輯 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 組態檔，以包含您 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫的連線資訊，並讓某個標記與您的工作流程處理常式組件產生關聯：  
  
1.  在 \<Your installation folder> \Master 資料 services\webapplication\bin 中尋找 Microsoft.MasterDataServices.Workflow.exe.config  
  
2.  將 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫連線資訊新增至 "ConnectionString" 設定。 如果您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝使用區分大小寫的定序，資料庫的名稱就必須以資料庫中相同的大小寫輸入。 例如，完整的設定標記可能如以下所示：  
  
    ```xml  
    <setting name="ConnectionString" serializeAs="String">  
        <value>Server=myServer;Database=myDatabase;Integrated Security=True</value>  
    </setting>  
    ```  
  
3.  在 "ConnectionString" 設定下方新增 "WorkflowTypeExtenders" 設定，讓標籤名稱與您的工作流程處理常式組件建立關聯。 例如：  
  
    ```xml  
    <setting name="WorkflowTypeExtenders" serializeAs="String">  
        <value>TEST=MDSWorkflowTestLib.WorkflowTester, MDSWorkflowTestLib</value>  
    </setting>  
    ```  
  
     標記的內部文字的 \<value> 格式為 \<Workflow tag> = \<assembly-qualified workflow type name> 。 \<Workflow tag>這是當您在中建立商務規則時，用來識別工作流程處理常式元件的名稱 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 。 \<assembly-qualified workflow type name>是您工作流程類別的命名空間限定名稱，後面接著逗號，後面接著元件的顯示名稱。 如果您的組件具備強式名稱，也必須包含版本資訊及其 PublicKeyToken。 \<setting>如果您已針對不同種類的工作流程建立多個工作流程處理常式，則可以包含多個標記。  
  
> [!NOTE]  
>  根據您伺服器的設定，可以在嘗試儲存 Microsoft.MasterDataServices.Workflow.exe.config 檔案時，看到「存取遭拒」錯誤。 如果發生這個情形，請暫時停用伺服器上的 [使用者帳戶控制 (UAC)]。 若要這麼做，開啟 [控制台]，然後按一下 [系統及安全性]****。 在 [控制中心]**** 底下，按一下 [變更使用者帳戶控制設定]****。 在 [使用者帳戶控制設定]**** 對話方塊中，將長條滑動到底部，讓您絕不會收到通知。 重新啟動電腦，然後重複以上的步驟以編輯您的組態檔。 儲存此檔案之後，將您的 UAC 設定重設為預設層級。  
  
### <a name="start-sql-server-mds-workflow-integration-service"></a>啟動 SQL Server MDS 工作流程整合服務  
 根據預設，不會安裝 SQL Server MDS 工作流程整合服務。 您必須先安裝此服務，才能使用它。 為獲得更大的安全性，請為服務建立本機使用者，並僅授與此使用者執行工作流程作業所需的權限。 若要建立使用者，請安裝服務、啟動服務，然後遵循以下步驟進行：  
  
1.  使用 [本機使用者和群組] 管理員建立區域使用者，例如， mds_workflow_service。  
  
2.  使用 SQL Server Management Studio 授與 mds_workflow_service 使用者權限以執行 [mdm].[udpExternalActionsGet] 預存程序。 若要這麼做，請為 mds_workflow_service account 建立一個新的登入，在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫中建立新使用者、將此使用者對應至 mds_workflow_service login，並授與使用者對於 [mdm].[udpExternalActionsGet] 預存程序的 EXECUTE 權限。  
  
3.  授與 mds_workflow_service 使用者權限以執行工作流程處理常式組件。 若要這麼做，請將 mds_workflow_service user 新增至工作流程處理常式組件之 [內容]**** 的 [安全性]**** 索引標籤，然後授與 mds_workflow_service user 的 READ 和 EXECUTE 權限。  
  
4.  授與 mds_workflow_service 使用者權限以執行 SQL Server MDS 工作流程整合服務可執行檔。 若要這麼做，請在 \Master 資料 Services\webapplication\bin) 中，將 mds_workflow_service 使用者新增至 Microsoft.MasterDataServices.Workflow.exe**屬性**的 [**安全性**] 索引標籤，並將 [ \<Your installation folder> 讀取] 和 [執行] 許可權授與 mds_workflow_service 使用者。  
  
5.  使用名稱為 InstallUtil.exe 的 .NET 安裝公用程式，安裝 SQL Server MDS 工作流程整合服務。 InstallUtil.exe 可以在 .NET 安裝資料夾 (例如 C:\Windows\Microsoft.NET\Framework\v4.0.30319\\) 中找到。 在提升權限的命令提示字元下輸入以下內容，安裝 SQL Server MDS 工作流程整合服務：  
  
    ```  
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil Microsoft.MasterDataServices.Workflow.exe  
    ```  
  
     在安裝期間出現提示時，指定 mds_workflow_service user。  
  
6.  使用 Services 嵌入式管理單元啟動 SQL Server MDS 工作流程整合服務。 若要這麼做，請在 Services 嵌入式管理單元中尋找 SQL Server MDS 工作流程整合服務，選取該服務，然後按一下 [啟動]**** 連結。  
  
### <a name="create-a-workflow-business-rule"></a>建立工作流程商務規則  
 使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 建立並發佈套用時啟動工作流程的商務規則。 您應該確定您的商務規則中包含變更屬性值的動作，讓規則在套用一次之後，評估為 false。 例如，當 Price 屬性值大於 500，且 Approved 屬性值為空白時，您的商務規則可能會評估為 true。 接著，此規則可能會包含兩個動作：一個是將 Approved 屬性值設定為 Pending，另一個是啟動工作流程。 或者，建議您建立一個使用「已變更」條件的規則，並新增您的屬性以變更追蹤群組。 如需商務規則的詳細資訊，請參閱[商務規則 &#40;Master Data Services&#41;](../business-rules-master-data-services.md)。  
  
 依照以下步驟，建立在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中啟動自訂工作流程的商務規則。  
  
1.  在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的商務規則編輯器中指定您商務規則的條件之後，將 [啟動工作流程]**** 動作從 [外部動作]**** 清單拖曳到 [THEN]**** 窗格的 [動作]**** 標籤中。  
  
2.  在 [編輯動作]**** 窗格的 [工作流程類型]**** 方塊中，輸入可識別您工作流程處理常式組件的標記。 這是您在組態檔中，為組件指定的標記，例如 TEST。  
  
3.  或者，選取 [包含成員資料]**** 核取方塊。 選擇此核取方塊以便在 XML 中包含傳遞至工作流程處理常式的屬性名稱和值。  
  
4.  在 [工作流程網站]**** 方塊中，鍵入網站的名稱。 這可能不適用於您的自訂工作流程，但是可用於加入的內容。  
  
5.  在 [工作流程名稱]**** 方塊中，從 Visual Studio 鍵入工作流程的名稱。 這可能不適用於您的自訂工作流程，但是可用於加入的內容。  
  
6.  儲存並發佈商務規則。  
  
### <a name="apply-business-rules-to-start-a-workflow"></a>套用商務規則以啟動工作流程  
 將商務規則套用至您的資料以啟動工作流程。 若要這麼做，請使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 編輯包含您要驗證之成員的實體。 按一下 [套用商務規則]****。 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 會擴展 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫的 Service Broker 佇列，以回應商務規則。 當 SQL Server MDS 工作流程整合服務檢查佇列時，會將資料傳送至指定的工作流程處理常式組件，然後清除佇列。 工作流程處理常式組件會執行您已經為其撰寫程式碼的動作。  
  
## <a name="troubleshoot-custom-workflows"></a>疑難排解自訂工作流程  
 如果您的工作流程處理常式組件沒有收到資料，可以嘗試為 SQL Server MDS 工作流程整合服務偵錯，或檢視 Service Broker 佇列。  
  
### <a name="debug-sql-server-mds-workflow-integration-service"></a>為 SQL Server MDS 工作流程整合服務偵錯  
 若要為 SQL Server 工作流程整合服務偵錯，請採取下列步驟：  
  
1.  使用服務嵌入式管理單元停止服務。  
  
2.  開啟命令提示字元、導覽到服務的位置，然後在主控台模式下輸入 Microsoft.MasterDataServices.Workflow.exe -console 來執行服務。  
  
3.  在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中，更新您的成員，然後再次套用商務規則。 詳細的記錄顯示在主控台視窗中。  
  
### <a name="view-the-service-broker-queue"></a>檢視 Service Broker 佇列  
 包含當做工作流程一部分傳遞之主資料的 Service Broker 佇列為：mdm.microsoft/mdm/queue/externalaction。 佇列可以在 SQL Management Studio **物件總管** 之 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫的 Service Broker 節點底下找到。 請注意，如果服務已正確清除佇列，此佇列將是空的。  
  
## <a name="see-also"></a>另請參閱  
 [自訂工作流程範例 &#40;Master Data Services&#41;](create-a-custom-workflow-example.md)   
 [自訂工作流程 XML 描述 &#40;Master Data Services&#41;](create-a-custom-workflow-xml-description.md)  
  
  
