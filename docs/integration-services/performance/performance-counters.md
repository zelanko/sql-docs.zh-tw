---
title: 效能計數器 | Microsoft Docs
ms.custom: supportability
ms.date: 08/27/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], performance counters
- performance counters [Integration Services]
- data flow [Integration Services], performance
- counters [Integration Services]
- data flow engine [Integration Services]
ms.assetid: 11e17f4e-72ed-44d7-a71d-a68937a78e4c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 431c88eb4f341b55060c23a06b06cf5e599c38e0
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918297"
---
# <a name="performance-counters"></a>效能計數器

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會安裝一組您可以用於監視資料流程引擎效能的效能計數器。 例如,，您可以監看 "Buffers spooled" 計數器以判斷是否要在封裝執行時，暫時將資料緩衝區寫入到磁碟中。 這種交換會降低效能，並指出電腦的記憶體不足。  
  
> **注意** ：如果您在執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的電腦上安裝 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]，然後將該電腦升級到 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]，則升級程序會從電腦中移除 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 效能計數器。 若要還原電腦上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 效能計數器，請在修復模式中執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。  
  
 下表描述這些效能計數器。  
  
|效能計數器|描述|  
|-------------------------|-----------------|  
|BLOB bytes read|資料流程引擎已從所有來源讀取之二進位大型物件 (BLOB) 資料的位元組數目。|  
|BLOB bytes written|資料流程引擎已寫入所有目的地之 BLOB 資料的位元組數目。|  
|BLOB files in use|資料流程引擎目前用於多工緩衝處理的 BLOB 檔案數目。|  
|Buffer memory|使用中的記憶體數量。 這可能同時包括實體和虛擬記憶體。 當這個數目大於實體記憶體的數量時， **Buffers Spooled** 計數會提高，這表示記憶體交換正在增加。 增加的記憶體交換會降低資料流程引擎的效能。|  
|Buffers in use|所有資料流程元件及資料流程引擎目前正在使用之所有類型的緩衝區物件數目。|  
|Buffers Spooled|目前已寫入磁碟的緩衝區數目。 如果資料流程引擎執行所用的實體記憶體偏低，則會將目前未使用的緩衝區寫入磁碟，然後在需要時重新載入。|  
|Flat buffer memory|所有一般緩衝區使用的記憶體總數 (以位元組為單位)。 一般緩衝區是元件用以儲存資料的記憶體區塊。 一般緩衝區是按位元組逐個存取的大型位元組區塊。|  
|Flat buffers in use|資料流程引擎所使用的一般緩衝區數目。 所有一般緩衝區都是私用緩衝區。|  
|Private buffer memory|所有私用緩衝區使用中的記憶體總數。 如果資料流程引擎建立緩衝區以支援資料流程，則該緩衝區就不是私用緩衝區。 私用緩衝區是轉換只將其用於暫存工作的緩衝區。 例如，「彙總」轉換使用私用緩衝區執行其工作。|  
|Private buffers in use|轉換所使用的緩衝區數目。|  
|Rows read|來源產生的資料列數目。 該數目不包括「查閱」轉換從參考資料表讀取的資料列。|  
|Rows written|提供給目的地的資料列數目。 該數目並不反映寫入目的地資料存放區的資料列。|  
  
 使用「效能 Microsoft Management Console (MMC)」嵌入式管理單元，可建立擷取效能計數器的記錄檔。  
  
 如需如何改善效能的資訊，請參閱 [資料流程效能的功能](../../integration-services/data-flow/data-flow-performance-features.md)。  
  
## <a name="obtain-performance-counter-statistics"></a>取得效能計數器統計資料  
 針對部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，您可以使用 [dm_execution_performance_counters &#40;SSISDB 資料庫&#41;](../../integration-services/functions-dm-execution-performance-counters.md) 函數取得效能計數器統計資料。  
  
 在下列範例中，函數會傳回識別碼為 34 之執行中執行作業的統計資料。  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
 在下列範例中，函數會傳回 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上執行之所有執行作業的統計資料。  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
> **重要！！** 如果您是 **ssis_admin** 資料庫角色的成員，則會傳回所有執行中之執行的效能統計資料。  如果您不是 **ssis_admin** 資料庫角色的成員，則會傳回您具有讀取權限之執行中執行的效能統計資料。  
  
## <a name="related-content"></a>相關內容  
  
-   codeplex.com 上的工具： [Business Intelligence Development Studio 的 SSIS 效能視覺化 (CodePlex 專案)](https://go.microsoft.com/fwlink/?LinkId=146626)。  
  
-   msdn.microsoft.com 上的影片： [測量與了解您企業中的 SSIS 封裝資料效能 (SQL Server 影片)](https://go.microsoft.com/fwlink/?LinkId=150497)。  
  
-   support.microsoft.com 上的技術支援文件： [升級至 Windows Server 2008 之後，效能監視器中無法再使用 SSIS 效能計數器](https://go.microsoft.com/fwlink/?LinkId=235319)(機器翻譯)。  

## <a name="add-a-log-for-data-flow-performance-counters"></a>加入資料流程效能計數器的記錄檔
  此程序描述如何加入資料流程引擎提供之效能計數器的記錄檔。  
  
> [!NOTE]  
>  ：如果您在執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的電腦上安裝 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]，然後將該電腦升級到 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]，則升級程序會從電腦中移除 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 效能計數器。 若要還原電腦上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 效能計數器，請在修復模式中執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。  
  
### <a name="to-add-logging-of-performance-counters"></a>若要加入效能計數器的記錄  
  
1.  在 [控制台] 中，如果使用傳統檢視，請按一下 [系統管理工具]。 如果使用類別檢視，請按一下 [效能及維護]，然後按一下 [系統管理工具]。  
  
2.  按一下 [效能]。  
  
3.  在 [效能] 對話方塊中，展開 [效能記錄檔及警示]，以滑鼠右鍵按一下 [計數器記錄檔]，然後按一下 [新記錄檔設定]。 鍵入記錄檔的名稱。 例如，輸入 **MyLog**。  
  
4.  按一下 [確定]。  
  
5.  在 [MyLog] 對話方塊中，按一下 [加入計數器]。  
  
6.  按一下 [使用本機電腦計數器]，以記錄本機電腦上的效能計數器，或按一下 [從下列電腦選取計數器]，然後從清單選取電腦，以記錄指定之電腦上的效能計數器。  
  
7.  在 [加入計數器] 對話方塊中，選取 [效能物件] 清單中的 [SQL Server:SSIS Pipeline]。  
  
8.  若要選取效能計數器，請執行下列其中之一：  
  
    -   選取 [所有計數器]，以記錄所有效能計數器。  
  
    -   選取 [從清單選取計數器]，並選取要使用的效能計數器。  
  
9. 按一下 [新增] 。  
  
10. 按一下 [關閉] 。  
  
11. 在 [MyLog] 對話方塊中，檢閱 [計數器] 清單中記錄效能計數器的清單。  
  
12. 若要加入其他計數器，請重複步驟 5 至 10。  
  
13. 按一下 [確定]。  
  
    > [!NOTE]  
    >  您必須使用 Administrators 群組成員的本機帳戶或網域帳戶，啟動「效能記錄檔及警示」服務。  

## <a name="see-also"></a>另請參閱  
 [執行專案與套件](../packages/run-integration-services-ssis-packages.md) [Integration Services 套件所記錄的事件](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
