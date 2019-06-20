---
title: 效能計數器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 79c9e433a6b5bcf9babee0060fdf028775e0e8a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62889832"
---
# <a name="performance-counters"></a>效能計數器
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會安裝一組您可以用於監視資料流程引擎效能的效能計數器。 例如,，您可以監看 "Buffers spooled" 計數器以判斷是否要在封裝執行時，暫時將資料緩衝區寫入到磁碟中。 這種交換會降低效能，並指出電腦的記憶體不足。  
  
> [!NOTE]  
>  如果您在執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的電腦上安裝 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]，然後將該電腦升級到 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]，則升級程序會從電腦中移除 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 效能計數器。 若要還原電腦上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 效能計數器，請在修復模式中執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。  
  
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
  
 如需如何改善效能的資訊，請參閱[資料流程效能的功能](../data-flow/data-flow-performance-features.md)。  
  
## <a name="obtain-performance-counter-statistics"></a>取得效能計數器統計資料  
 針對部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，您可以使用 [dm_execution_performance_counters &#40;SSISDB 資料庫&#41;](/sql/integration-services/functions-dm-execution-performance-counters) 函數取得效能計數器統計資料。  
  
 在下列範例中，函數會傳回識別碼為 34 之執行中執行作業的統計資料。  
  
```  
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
 在下列範例中，函數會傳回 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上執行之所有執行作業的統計資料。  
  
```  
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
> [!IMPORTANT]  
>  如果您是 `ssis_admin` 資料庫角色的成員，則會傳回所有執行中之執行的效能統計資料。  如果您不是 `ssis_admin` 資料庫角色的成員，則會傳回您具有讀取權限之執行中執行的效能統計資料。  
  
## <a name="related-content"></a>相關內容  
  
-   codeplex.com 上的工具：[Business Intelligence Development Studio 的 SSIS 效能視覺化 (CodePlex 專案)](https://go.microsoft.com/fwlink/?LinkId=146626)。  
  
-   msdn.microsoft.com 上的影片：[測量與了解您企業中的 SSIS 封裝資料效能 (SQL Server 影片)](https://go.microsoft.com/fwlink/?LinkId=150497)。  
  
-   support.microsoft.com 上的技術支援文件： [升級至 Windows Server 2008 之後，效能監視器中無法再使用 SSIS 效能計數器](https://go.microsoft.com/fwlink/?LinkId=235319)(機器翻譯)。  
  
## <a name="see-also"></a>另請參閱  
 [執行專案和封裝](../packages/run-integration-services-ssis-packages.md)  
  
  
