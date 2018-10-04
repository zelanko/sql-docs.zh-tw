---
title: Web 服務工作編輯器 （輸出頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e2a0c1639352b8c5aaad9be4bd6740eceacb6cf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132008"
---
# <a name="web-service-task-editor-output-page"></a>Web 服務工作編輯器 (輸出頁面)
  使用 [Web 服務工作編輯器] 對話方塊的 [輸出] 頁面，即可指定 Web 方法傳回的結果之儲存位置。  
  
 若要了解這個工作，請參閱 [Web 服務工作](control-flow/web-service-task.md)。  
  
## <a name="static-options"></a>靜態選項  
 **OutputType**  
 選取儲存結果時使用的儲存類型。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**檔案連接**|在檔案中儲存結果。 選取此值會顯示動態選項 [檔案]。|  
|**變數**|在變數中儲存結果。 選取此值會顯示動態選項 [變數]。|  
  
## <a name="outputtype-dynamic-options"></a>OutputType 動態選項  
  
### <a name="outputtype--file-connection"></a>OutputType = 檔案連接  
 **檔案**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連線...>]，即可建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="outputtype--variable"></a>OutputType = 變數  
 **變數**  
 在清單中選取變數，或按一下 [\<新增變數...>]，以建立新的變數。  
  
 **相關主題：**[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Web 服務工作編輯器&#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [Web 服務工作編輯器&#40;輸入頁面&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [運算式頁面](expressions/expressions-page.md)  
  
  
