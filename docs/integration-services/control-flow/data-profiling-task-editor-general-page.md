---
title: 資料分析工作編輯器 (一般頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataprofilingtask.general.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: eec15906-d757-4079-b2f6-aca4e52b3b4c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5e8f03d8978056ecd0faefd247163d2806dc7988
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290484"
---
# <a name="data-profiling-task-editor-general-page"></a>資料分析工作編輯器 (一般頁面)
  您可以使用 [資料分析工作編輯器] 的 [一般] 頁面來設定下列選項：  
  
-   指定設定檔輸出的目的地。  
  
-   使用預設設定來簡化分析單一資料表或檢視表的工作。  
  
 如需如何使用資料分析工作的詳細資訊，請參閱 [資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。 如需如何使用資料設定檔檢視器來分析資料分析工作輸出的詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
 **開啟資料分析工作編輯器的一般頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟具有資料分析工作的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [控制流程] 索引標籤中，按兩下資料分析工作。  
  
3.  在 [資料分析工作編輯器] 中，按一下 [一般]。  
  
## <a name="data-profiling-options"></a>資料分析選項  
 **逾時**  
 指定資料分析工作應該逾時並停止執行之前經過的秒數。 預設值為 0，表示沒有逾時。  
  
## <a name="destination-options"></a>目的地選項  
  
> [!IMPORTANT]  
>  輸出檔可能包含您資料庫的相關敏感性資料，以及資料庫所包含的資料。 如需如何讓這個檔案更安全的相關建議，請參閱 [對封裝使用之檔案的存取權](../../integration-services/security/security-overview-integration-services.md#files)。  
  
 **DestinationType**  
 指定要將資料設定檔輸出儲存至檔案或變數：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**FileConnection**|將設定檔輸出儲存至檔案連線管理員中指定之位置的檔案。<br /><br /> 注意：您可以在 [目的地] 選項中指定要使用的檔案連線管理員。|  
|**變數**|將設定檔輸出儲存至封裝變數。<br /><br /> 注意：您可以在 [目的地] 選項中指定要使用的封裝變數。|  
  
 **目的地**  
 指定哪一個檔案連線管理員或封裝變數包含資料設定檔輸出：  
  
-   如果 [DestinationType] 選項設定為 [FileConnection]，[目的地] 選項就會顯示可用的檔案連線管理員。 您可以選取其中一個連線管理員，或選取 [\<新增檔案連線>] 來建立新的檔案連線管理員。  
  
-   如果 [DestinationType] 選項設定為 [變數]，[目的地] 選項就會在 [目的地] 清單中顯示可用的封裝變數。 您可以選取其中一個變數，或選取 [\<新增變數>] 來建立新的變數。  
  
 **OverwriteDestination**  
 指定是否要覆寫輸出檔 (如果它已經存在的話)。 預設值為 **[False]**。 只有當 [DestinationType] 選項設定為 [FileConnection] 時，系統才會使用這個屬性的值。 當 [DestinationType] 選項設定為 [變數] 時，此工作永遠會覆寫變數的上一個值。  
  
> [!IMPORTANT]  
>  如果您嘗試執行資料分析工作一次以上，但不變更輸出檔名稱或將 **OverwriteDestination** 屬性的值變更為 **True**，此工作便會失敗，並顯示輸出檔已經存在的訊息。  
  
## <a name="other-options"></a>其他選項  
 **快速分析**  
 顯示 [單一資料表快速分析表單]。 這個表單會簡化使用預設設定來分析單一資料表或檢視表的工作。 如需詳細資訊，請參閱 [單一資料表快速分析表單 &#40;資料分析工作&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)。  
  
 **開啟設定檔檢視器**  
 開啟資料設定檔檢視器。 獨立資料設定檔檢視器會顯示資料分析工作的資料設定檔輸出。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝內部執行資料分析工作並計算資料設定檔後，您可以檢視資料設定檔輸出。  
  
> [!NOTE]  
>  您也可以藉由執行 \<磁碟機>:\Program Files (x86) | Program Files\Microsoft SQL Server\110\DTS\Binn 資料夾中的 DataProfileViewer.exe，開啟資料設定檔檢視器。  
  
## <a name="see-also"></a>另請參閱  
 [單一資料表快速分析表單 &#40;資料分析工作&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)   
 [資料分析工作編輯器 &#40;設定檔要求頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
  
  
