---
title: "排程 SSAS 管理工作，與 SQL Server Agent |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d1484b3-51d9-48a0-93d2-0c3e4ed22b87
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 857540f661aa8eaecd42d98a648c03c043d06e2a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="schedule-ssas-administrative-tasks-with-sql-server-agent"></a>使用 SQL Server Agent 排程 SSAS 管理工作
  您可以使用 SQL Server Agent 服務來為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理工作排程，以便按照所需的順序和時間執行工作。 為工作排程可協助您將處理自動化，以便定期或依照可預測的週期執行。 您可以排程管理工作 (例如 Cube 處理) 在商務活動較少的時間執行。 此外，您也可以在 SQL Server Agent 作業內建立作業步驟，決定工作執行的順序。 例如，您可以先處理 Cube，然後再執行 Cube 的備份。  
  
 作業步驟可以讓您控制執行的流程。 如果一項作業失敗，您可以設定 SQL Server Agent 繼續執行其餘工作或停止執行。 您也可以設定 SQL Server Agent 傳送有關作業執行成功或失敗的通知。  
  
 本主題是一項逐步解說，其中示範了兩種使用 SQL Server Agent 來執行 XMLA 指令碼的方式。 第一則範例會示範如何排程單一維度的處理。 第二則範例會示範如何將處理工作結合成依照排程執行的單一指令碼。 若要完成此逐步解說，您必須符合下列必要條件。  
  
## <a name="prerequisites"></a>必要條件  
 您必須安裝 SQL Server Agent 服務。  
  
 根據預設，作業會在此服務帳戶底下執行。 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，SQL Server Agent 的預設帳戶是 NT Service\SQLAgent$\<執行個體名稱 >。 若要執行備份或處理工作，此帳戶必須是 Analysis Services 執行個體的系統管理員。 如需詳細資訊，請參閱 [將伺服器系統管理員權限授與 Analysis Services 執行個體](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)。  
  
 您也應該擁有要使用的測試資料庫。 您可以部署 AdventureWorks 多維度範例資料庫或是要用於此逐步解說之 Analysis Services 多維度教學課程中的專案。 如需詳細資訊，請參閱 [安裝 Analysis Services 多維度模型化教學課程的範例資料和專案](../../analysis-services/install-sample-data-and-projects.md)。  
  
## <a name="example-1-processing-a-dimension-in-a-scheduled-task"></a>範例 1：在排程工作中處理維度  
 這則範例會示範如何建立和排程處理維度的作業。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 排程工作是內嵌至 SQL Server Agent 作業中的 XMLA 指令碼。 這項作業已排程在所要的時間與頻率執行。 由於 SQL Server Agent 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的一部分，因此，您會同時使用 Database Engine 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 來建立並排程管理工作。  
  
###  <a name="bkmk_CreateScript"></a> 在 SQL Server Agent 作業中建立處理維度的指令碼  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 開啟資料庫資料夾並尋找維度。 以滑鼠右鍵按一下維度，然後選取 [處理]。  
  
2.  在 **[處理維度]** 對話方塊中，於 **[物件清單]** 下的 **[處理選項]**資料行中，確認這個資料行的選項是 **[完整處理]**。 如果不是，請在 [處理選項] 底下，按一下選項，然後從下拉式清單中選取 [完整處理]。  
  
3.  按一下 **[指令碼]**。  
  
     此步驟會開啟包含處理維度之 XMLA 指令碼的 **[XML 查詢]** 視窗。  
  
4.  在 **[處理維度]** 對話方塊中，按一下 **[取消]** 關閉對話方塊。  
  
5.  在 [XMLA 查詢] 視窗中，反白顯示 XMLA 指令碼、以滑鼠右鍵按一下反白顯示的指令碼，然後選取 [複製]。  
  
     此步驟會將 XMLA 指令碼複製到 Windows [剪貼簿]。 您可以將 XMLA 指令碼保留在 [剪貼簿] 中，也可以將它貼入 [記事本] 或其他文字編輯器。 下面是 XMLA 指令碼的範例。  
  
    ```  
    <Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Account</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
###  <a name="bkmk_ProcessJob"></a> 建立和排程維度處理作業  
  
1.  連接到 Database Engine 的執行個體，然後開啟 [物件總管]。  
  
2.  展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 [作業]，然後選取 [新增作業]。  
  
4.  在 **[新增作業]** 對話方塊的 **[名稱]**方塊中，輸入作業名稱。  
  
5.  在 **[選取頁面]**底下，選取 **[步驟]**，然後按一下 **[新增]**。  
  
6.  在 **[新增作業步驟]** 對話方塊的 **[步驟名稱]**中，輸入步驟名稱。  
  
7.  在 [伺服器] 中，輸入 **localhost** (代表 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的預設執行個體) 和 **localhost\\**\<執行個體名稱> (代表具名執行個體)。  
  
     如果您要從遠端電腦執行作業，請使用作業執行所在的伺服器名稱和執行個體名稱。 使用格式\<*伺服器名稱*> 預設執行個體，和\<*伺服器名稱*>\\<*執行個體名稱*> 的具名執行個體。  
  
8.  在 **[類型]**中，選取 **[SQL Server Analysis Services 命令]**。  
  
9. 在 [命令] 中，按一下滑鼠右鍵，然後選取 [貼上]。 您在上一個步驟中產生的 XMLA 指令碼應該就會出現在命令視窗中。  
  
10. 按一下 **[確定]**。  
  
11. 在 **[選取頁面]**底下，按一下 **[排程]**，然後按一下 **[新增]**。  
  
12. 在 **[新增作業排程]** 對話方塊的 **[名稱]**中，輸入排程名稱，然後按一下 **[確定]**。  
  
     此步驟會建立星期日上午 12:00 的排程。 下一個步驟將為您示範如何手動執行作業。 您也可以指定在監視時執行作業的排程。  
  
13. 在 **[新增作業]** 對話方塊中，按一下 **[確定]**。  
  
14. 在物件總管中，展開 [作業]、以滑鼠右鍵按一下您所建立的作業，然後選取 [從下列步驟啟動作業]。  
  
     因為作業只有一個步驟，所以作業將立即執行。 如果作業包含多個步驟，您就可以選取應該啟動作業的步驟。  
  
15. 當作業完成時，請按一下 **[關閉]**。  
  
## <a name="example-2-batch-processing-a-dimension-and-a-partition-in-a-scheduled-task"></a>範例 2：在排程工作中批次處理維度和資料分割  
 這則範例中的程序會示範如何建立和排程批次處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫維度的作業，同時處理相依於此維度進行彙總的 Cube 資料分割。 如需批次處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的詳細資訊，請參閱[批次處理 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)。  
  
###  <a name="bkmk_BatchProcess"></a> 在 SQL Server Agent 作業中建立批次處理維度和資料分割的指令碼  
  
1.  使用相同的資料庫時，展開 [維度]、以滑鼠右鍵按一下 [客戶] 維度，然後選取 [處理]。  
  
2.  在 **[處理維度]** 對話方塊中，於 **[物件清單]** 下的 **[處理選項]**資料行中，確認這個資料行的選項是 **[完整處理]**。  
  
3.  按一下 **[指令碼]**。  
  
     此步驟會開啟包含處理維度之 XMLA 指令碼的 **[XML 查詢]** 視窗。  
  
4.  在 **[處理維度]** 對話方塊中，按一下 **[取消]** 關閉對話方塊。  
  
5.  依序展開 [Cube]、[Adventure Works]、[量值群組]、[網際網路銷售] 和 [資料分割]、以滑鼠右鍵按一下清單中的最後一個資料分割，然後選取 [處理]。  
  
6.  在 **[處理資料分割]** 對話方塊中，於 **[物件清單]** 下的 **[處理選項]**資料行中，確認這個資料行的選項是 **[完整處理]**。  
  
7.  按一下 **[指令碼]**。  
  
     此步驟會開啟第二個 **[XML 查詢]** 視窗，其中包含處理資料分割的 XMLA 指令碼。  
  
8.  在 **[處理資料分割]** 對話方塊中，按一下 **[取消]** 關閉編輯器。  
  
     此時，您必須合併這兩個指令碼，並且確保系統先處理維度。  
  
    > [!WARNING]  
    >  如果系統先處理資料分割，後續的維度處理就會導致資料分割變成尚未處理。 然後，資料分割需要第二次處理，才能達成已處理狀態。  
  
9. 在包含處理資料分割之 XMLA 指令碼的 [XMLA 查詢] 視窗中，反白顯示 `Batch` 和 `Parallel` 標記內部的程式碼、以滑鼠右鍵按一下反白顯示的指令碼，然後選取 [複製]。  
  
    ```  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID> Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
    ```  
  
10. 開啟包含處理維度之 XMLA 指令碼的 **[XMLA 查詢]** 視窗。 在 `</Process>` 標記左邊的指令碼中按一下滑鼠右鍵，然後選取 [貼上]。  
  
     下列範例顯示已修訂的 XMLA 指令碼。  
  
    ```  
    <Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Customer</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
11. 反白顯示已修訂的 XMLA 指令碼、以滑鼠右鍵按一下反白顯示的指令碼，然後選取 [複製]。  
  
12. 此步驟會將 XMLA 指令碼複製到 Windows [剪貼簿]。 您可以將 XMLA 指令碼保留在 [剪貼簿] 中、將它儲存至檔案，也可以將它貼入 [記事本] 或其他文字編輯器。  
  
###  <a name="bkmk_Scheduling"></a> 建立和排程批次處理作業  
  
1.  連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體，然後開啟 [物件總管]。  
  
2.  展開 **[SQL Server Agent]**。 如果此服務並未執行，請啟動它。  
  
3.  以滑鼠右鍵按一下 [作業]，然後選取 [新增作業]。  
  
4.  在 **[新增作業]** 對話方塊的 **[名稱]**方塊中，輸入作業名稱。  
  
5.  在 **[步驟]**中，按一下 **[新增]**。  
  
6.  在 **[新增作業步驟]** 對話方塊的 **[步驟名稱]**中，輸入步驟名稱。  
  
7.  在 **[類型]**中，選取 **[SQL Server Analysis Services 命令]**。  
  
8.  在 **[執行身分]**中，選取 **[SQL Server Agent 服務帳戶]**。 正如＜必要條件＞一節所述，此帳戶必須擁有 Analysis Services 的系統管理權限。  
  
9. 在 **[伺服器]**中，指定 Analysis Services 執行個體的伺服器名稱。  
  
10. 在 [命令] 中，按一下滑鼠右鍵，然後選取 [貼上]。  
  
11. 按一下 **[確定]**。  
  
12. 在 **[排程]** 頁面中，按一下 **[新增]**。  
  
13. 在 **[新增作業排程]** 對話方塊的 **[名稱]**中，輸入排程名稱，然後按一下 **[確定]**。  
  
     此步驟會建立星期日上午 12:00 的排程。 下一個步驟將為您示範如何手動執行作業。 您也可以選取在監視時執行作業的排程。  
  
14. 按一下 **[確定]** ，關閉對話方塊。  
  
15. 在物件總管中，展開 [作業]、以滑鼠右鍵按一下您所建立的作業，然後選取 [從下列步驟啟動作業]。  
  
     因為作業只有一個步驟，所以作業將立即執行。 如果作業包含多個步驟，您就可以選取應該啟動作業的步驟。  
  
16. 當作業完成時，請按一下 **[關閉]**。  
  
## <a name="see-also"></a>另請參閱  
 [處理選項和設定 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)   
  
  

