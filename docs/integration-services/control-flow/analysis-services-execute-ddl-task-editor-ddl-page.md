---
title: "Analysis Services 執行 DDL 工作編輯器 （DDL 頁面） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4bae07f66d84f8a692ad7b59ef61ee63d4a5fd62
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Analysis Services 執行 DDL 工作編輯器 (DDL 頁面)
  使用 [Analysis Services 執行 DDL 工作編輯器] 對話方塊的 [DDL] 頁面，即可指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的連接，並提供資料定義語言 (DDL) 陳述式來源的相關資訊。  
  
 若要了解這個工作，請參閱＜ [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)＞。  
  
## <a name="static-options"></a>靜態選項  
 **連接**  
 選取[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案或[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]連接管理員 中的清單或按一下\<**新增連接...**>，並使用**加入 Analysis Services 連接管理員**對話方塊，即可建立新的連接。  
  
 **相關主題：** [加入 Analysis Services 連線管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)、 [Analysis Services 連線管理員](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 指定 DDL 陳述式的來源類型。 此屬性具有下表所列的選項：  
  
|Value|說明|  
|-----------|-----------------|  
|**直接輸入**|將來源設定為 [SourceDirect] 文字方塊中所儲存的 DDL 陳述式。 選取這個值就會顯示在下列章節中的動態選項。|  
|**檔案連接**|將來源設定為包含 DDL 陳述式的檔案。 選取這個值就會顯示在下列章節中的動態選項。|  
|**變數**|將來源設定為變數。 選取這個值就會顯示在下列章節中的動態選項。|  
  
## <a name="dynamic-options"></a>動態選項  
  
### <a name="sourcetype--direct-input"></a>SourceType = 直接輸入  
 **Source**  
 輸入 DDL 陳述式或按一下省略符號 **(…)**，然後在 [DDL 陳述式] 對話方塊中輸入陳述式。  
  
### <a name="sourcetype--file-connection"></a>SourceType = 檔案連接  
 **Source**  
 在清單中，選取檔案連接，或按一下\<**新增連接...**>，並使用**檔案 」 連接管理員**對話方塊，即可建立新的連接。  
  
 **相關主題：**[檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = 變數  
 **Source**  
 在清單中，選取變數，或按一下\<**新增變數...**>，並使用**加入變數**對話方塊，即可建立新的變數。  
  
 **相關主題：**[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services 執行 DDL 工作編輯器 &#40;一般頁面 &#41;](../../integration-services/control-flow/analysis-services-execute-ddl-task-editor-general-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)   
 [Analysis Services 指令碼語言 &#40;ASSL for XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [XML for Analysis &#40;XMLA &#41;參考](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
