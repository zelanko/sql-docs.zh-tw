---
title: Analysis Services 執行 DDL 工作編輯器 （DDL 頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a4ebac7cac4a62dde5c89aa3e37146c78eb79d19
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535426"
---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Analysis Services 執行 DDL 工作編輯器 (DDL 頁面)
  使用 [Analysis Services 執行 DDL 工作編輯器] 對話方塊的 [DDL] 頁面，即可指定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫的連接，並提供資料定義語言 (DDL) 陳述式來源的相關資訊。  
  
 若要了解這個工作，請參閱＜ [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md)＞。  
  
## <a name="static-options"></a>靜態選項  
 **[連接]**  
 選取清單中的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 連線管理員，或是按一下 [\<新增連線...>] 並使用 [新增 Analysis Services 連線管理員] 對話方塊，即可建立新的連線。  
  
 **相關的主題：**[加入 Analysis Services 連接管理員對話方塊 UI 參考](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)， [Analysis Services 連線管理員](connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 指定 DDL 陳述式的來源類型。 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**直接輸入**|將來源設定為 [SourceDirect] 文字方塊中所儲存的 DDL 陳述式。 選取這個值就會顯示在下列章節中的動態選項。|  
|**檔案連接**|將來源設定為包含 DDL 陳述式的檔案。 選取這個值就會顯示在下列章節中的動態選項。|  
|**變數**|將來源設定為變數。 選取這個值就會顯示在下列章節中的動態選項。|  
  
## <a name="dynamic-options"></a>動態選項  
  
### <a name="sourcetype--direct-input"></a>SourceType = 直接輸入  
 **Source**  
 鍵入 DDL 陳述式或按一下省略符號 **(...)**，然後在 [DDL 陳述式] 對話方塊中鍵入陳述式。  
  
### <a name="sourcetype--file-connection"></a>SourceType = 檔案連接  
 **Source**  
 選取清單中的 [檔案連線]，或是按一下 [\<新增連線...>] 再使用 [檔案連線管理員] 對話方塊，即可建立新的連線。  
  
 **相關的主題：**[檔案連線管理員](connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = 變數  
 **Source**  
 在清單中選取變數，或按一下 [\<新增變數...>] 並使用 [新增變數] 對話方塊，以建立新的變數。  
  
 **相關的主題：**[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services 執行 DDL 工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [控制流程](control-flow/control-flow.md)   
 [Analysis Services 指令碼語言&#40;ASSL&#41;參考](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [XML for Analysis &#40;XMLA&#41; 參考](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)  
  
  
