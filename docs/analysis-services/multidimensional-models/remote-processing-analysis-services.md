---
title: 遠端處理 (Analysis Services) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e59011361e6dad623fa5f5cab71d262eb5eb8338
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="remote-processing-analysis-services"></a>遠端處理 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以執行遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的排程處理或自動處理，其只會處理某電腦所發出的要求，但會在同一網路中的另一部電腦上執行。  
  
## <a name="prerequisites"></a>必要條件  
  
-   您的每部電腦上若各自執行不同版本的 SQL Server，則用戶端程式庫的版本與處理此模型之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的版本必須相符。
  
-   遠端伺服器必須啟用 [允許遠端連線到此電腦]  ，而發出處理要求的帳戶必須列名為允許的使用者。  
  
-   Windows 防火牆規則必須設定為允許 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的傳入連線。 確認您可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接遠端 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行個體。 請參閱 [設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
-   解決現有的本機處理錯誤，然後再嘗試遠端處理。 確認當處理要求來自本機時，可以順利從外部關聯式資料來源擷取資料。 如需指定用來擷取資料之認證相關指示，請參閱[設定模擬選項 (SSAS - 多維度)](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)。  
  
## <a name="on-demand-remote-processing"></a>隨選遠端處理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]接受來自使用者或應用程式帳戶所擁有的處理要求[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]系統管理員權限。 您若是系統管理員，請確認您可以連接到遠端執行個體，並可透過遠端連接手動處理資料庫。  
  
1.  在要用於排程處理電腦上啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，並連接到遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
2.  在資料庫上按一下滑鼠右鍵，再選取 [處理序] 並指向 [指令碼]，然後選擇 [編寫動作的指令碼至新增查詢視窗]。 用於叫用處理的命令會出現在查詢視窗中。  
  
3.  按一下 [確定]  開始執行處理序。  
  
     此工作若是成功，將會提供 XMLA 查詢讓您嵌入排程的作業中。 此工作也會確認連接沒有問題。  
  
## <a name="schedule-remote-processing-using-sql-server-agent-service"></a>使用 SQL Server Agent 服務排程遠端處理  
 SQL Server Agent 服務預設會以虛擬帳戶執行，並使用電腦帳戶所建立的網路連接。 為避免授與遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上之電腦帳戶的系統管理權限，應將 SQL Server Agent 服務變更為以最低權限的網域使用者帳戶身分執行。  
  
 請務必授與帳戶所有必要的權限，包括提供此服務之 Database Engine 執行個體的 **sysadmin** 權限。  
  
 您可以使用下列連結來設定權限：  
  
-   [設定 SQL Server Agent](http://msdn.microsoft.com/library/2e361a62-9e92-4fcd-80d7-d6960f127900)  
  
-   若無法授與[SQL Server Agent Components](http://msdn.microsoft.com/library/8d1dc600-aabb-416f-b3af-fbc9fccfd0ec) 權限， **SQL Server Agent Components** 建議使用替代的固定伺服器角色。  
  
 設定帳戶權限之後，請繼續執行下列步驟。  
  
#### <a name="grant-the-sql-server-agent-account-administrator-permission-on-ssas"></a>授與 SSAS 上之 SQL Server Agent 帳戶的系統管理員權限  
  
1.  使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]連接到遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
2.  在伺服器名稱上按一下滑鼠右鍵，再按一下 [屬性]，然後按一下 [安全性]。  
  
3.  按一下 [加入]  ，以加入 SQL Server Agent 帳戶。  
  
#### <a name="create-the-job"></a>建立作業  
  
1.  在 Management Studio 中，連接到本機 Database Engine 執行個體。 SQL Server Agent 是物件總管中的最後一個項目。 如有必要，請啟動該服務。  
  
2.  在 [作業] 上按一下滑鼠右鍵，再按一下 [新增作業]，然後輸入名稱。  
  
3.  在步驟中按一下 [新增]  ，然後輸入名稱。  
  
4.  在 [類型] 中，選取 [SQL Server Analysis Services 命令] 。  
  
5.  在 [伺服器] 中，輸入遠端名稱 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。  
  
6.  在 [命令] 中，貼上用以處理資料庫的 XMLA 命令。 這就是您在隨選遠端處理之驗證步驟中所產生的 XMLA 指令碼。 按一下 **[確定]** 以儲存作業。  
  
#### <a name="start-sql-server-profiler"></a>啟動 SQL Server Profiler  
  
1.  在遠端電腦上，啟動 SQL Server Profiler。 連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，然後按一下 [執行]  ，以啟動使用預設事件的追蹤。  
  
     您將使用 SQL Server Profiler 監視所發生旳處理事件。  
  
2.  (選擇性) 您可以設定追蹤屬性，將追蹤傳送至檔案或資料庫中的資料表。  
  
#### <a name="run-the-job"></a>執行作業  
  
1.  在執行此作業的電腦上，確認此作業可以執行基本作業。 在物件總管中的 SQL Server Agent 下，先展開 [作業]，再於剛才所建立的作業上按一下滑鼠右鍵，然後按一下 [從下列步驟啟動作業]。 作業會立即啟動。 您可以在 SQL Server Profiler 中監視進度。  
  
2.  最後一個步驟是將作業修改成依照您所義的排程執行，並新增管理作業所需的警示或通知。 您也可能想要精簡處理指令碼，或在作業中建立多個步驟來單獨處理物件。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 元件](http://msdn.microsoft.com/library/8d1dc600-aabb-416f-b3af-fbc9fccfd0ec)   
 [使用 SQL Server Agent 排程 SSAS 管理工作](../../analysis-services/instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)   
 [批次處理 & #40;Analysis Services & #41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)   
 [處理多維度模型 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [處理物件 & #40;XMLA & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)  
  
  
