---
title: "Analysis Services 處理工作編輯器 （Analysis Services 頁面） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing Task Editor
ms.assetid: 5612be78-57cf-4e4e-92cf-6bfa9f971040
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e5b90a26fb4477243c5a48b87d134ff8129430ab
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Analysis Services 處理工作編輯器 (Analysis Services 頁面)
  使用 [Analysis Services 處理工作編輯器] 對話方塊的 [Analysis Services] 頁面，即可指定 Analysis Services 連接管理員、選取要處理的分析物件，以及設定處理與錯誤處理選項。  
  
 處理表格式模型時，請牢記以下事項：  
  
1.  您無法在表格式模型上執行影響分析。  
  
2.  系統不會公開表格式模型的部分處理選項，例如 [處理重組] 和 [處理重新計算]。 您可以使用「執行 DLL」工作，執行這些功能。  
  
3.  提供的部分處理選項 (例如處理索引) 不適合表格式模型，因此應該不會使用。  
  
4.  表格式模型會忽略批次處理設定。  
  
 若要了解這個工作，請參閱 [Analysis Services 處理工作](../../integration-services/control-flow/analysis-services-processing-task.md)。  
  
## <a name="options"></a>選項。  
 **Analysis Services 連接管理員**  
 在清單中選取現有的 Analysis Services 連接管理員，或按一下 [新增] 以建立新的連接管理員。  
  
 **新**  
 建立新的 Analysis Services 連接管理員。  
  
 **相關主題：** [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)、 [加入 Analysis Services 連接管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **物件清單**  
 |屬性|說明|  
|--------------|-----------------|  
|**Object Name**|列出指定的物件名稱。|  
|**型別**|列出指定的物件類型。|  
|**處理選項**|選取清單中的處理選項。<br /><br /> **相關主題：**[處理多維度模型 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)|  
|**[設定]**|列出指定物件的處理設定。|  
  
 **加入**  
 將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件加入清單中。  
  
 **移除**  
 選取物件，然後按一下 [刪除]。  
  
 **影響分析**  
 執行選取之物件的影響分析。  
  
 **相關主題：**[影響分析對話方塊 &#40;Analysis Services - 多維度資料&#41;](http://msdn.microsoft.com/library/208268eb-4e14-44db-9c64-6f74b776adb6)  
  
 **批次設定摘要**  
 |屬性|說明|  
|--------------|-----------------|  
|**處理順序**|指定循序地或在批次中處理物件；如果使用平行處理，請指定要並行處理的物件數目。|  
|**交易模式**|指定循序處理的交易模式。|  
|**維度錯誤**|指定發生錯誤時的工作行為。|  
|**維度索引鍵錯誤記錄路徑**|指定記錄錯誤的檔案路徑。|  
|**處理受影響的物件**|指出是否也處理相依物件或受影響的物件。|  
  
 **變更設定**  
 變更維度索引鍵中的處理選項和錯誤處理。  
  
 **相關主題：**[變更設定對話方塊 &#40;Analysis Services - 多維度資料&#41;](http://msdn.microsoft.com/library/0041e042-d7ce-48f9-a690-a6dc65471ff3)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services 處理工作編輯器 &#40;一般頁面 &#41;](../../integration-services/control-flow/analysis-services-processing-task-editor-general-page.md)   
 [Analysis Services 執行 DDL 工作](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
  
