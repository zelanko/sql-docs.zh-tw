---
title: "Web 服務工作編輯器 (輸出頁面) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.webservicestask.output.f1"
helpviewer_keywords: 
  - "Web 服務工作編輯器"
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Web 服務工作編輯器 (輸出頁面)
  使用 [Web 服務工作編輯器] 對話方塊的 [輸出] 頁面，即可指定 Web 方法傳回的結果之儲存位置。  
  
 若要了解這個工作，請參閱 [Web 服務工作](../../integration-services/control-flow/web-service-task.md)。  
  
## 靜態選項  
 **OutputType**  
 選取儲存結果時使用的儲存類型。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**檔案連接**|在檔案中儲存結果。 選取此值會顯示動態選項 [檔案]。|  
|**變數**|在變數中儲存結果。 選取此值會顯示動態選項 [變數]。|  
  
## OutputType 動態選項  
  
### OutputType = 檔案連接  
 **檔案**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連接...>]，即可建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### OutputType = 變數  
 **變數**  
 在清單中選取變數，或按一下 [\<新增變數...>]，以建立新的變數。  
  
 **相關主題：**[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](../Topic/Add%20Variable.md)  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [Web 服務工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/web-service-task-editor-general-page.md)   
 [Web 服務工作編輯器 &#40;輸入頁面&#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
  