---
title: 執行處理工作編輯器 （處理頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.process.f1
helpviewer_keywords:
- Execute Process Task Editor
ms.assetid: 0fc22406-e79b-47a4-a7e4-108d4ce6202f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa799404777f8f0ef0a8a07a81c8c7961c636004
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059024"
---
# <a name="execute-process-task-editor-process-page"></a>執行處理工作編輯器 (處理頁面)
  使用 **[執行處理工作編輯器]** 對話方塊的 **[處理]** 頁面，即可設定執行處理的選項。 這些選項包括要執行的可執行檔、其位置、命令提示字元引數，以及提供輸入和擷取輸出的變數。  
  
 若要了解這個工作，請參閱＜ [Execute Process Task](control-flow/execute-process-task.md)＞。  
  
## <a name="options"></a>選項  
 **RequireFullFileName**  
 指出如果在指定位置找不到可執行檔時，工作是否失敗。  
  
 **可執行檔**  
 輸入要執行的可執行檔名稱。  
  
 **引數**  
 提供命令提示字元引數。  
  
 **WorkingDirectory**  
 鍵入包含可執行檔的資料夾路徑，或按一下瀏覽按鈕 **(...)** 並尋找資料夾。  
  
 **StandardInputVariable**  
 選取變數來提供處理序的輸入，或按一下 [\<新增變數...>]  建立新的變數：  
  
 **相關主題：** [新增變數](../../2014/integration-services/add-variable.md)  
  
 **StandardOutputVariable**  
 選取變數來擷取處理序的輸出，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **StandardErrorVariable**  
 選取變數來擷取處理器的錯誤輸出，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 指出如果處理序的結束碼和 **SuccessValue**中指定的值不同時，工作是否失敗。  
  
 **SuccessValue**  
 指定可執行檔要表示成功時將傳回的值。 依預設，此值設定為 **0**。  
  
 **TimeOut**  
 指定處理序可以執行的秒數。 若值為 **0** ，表示不使用逾時值，則處理序會一直執行到完成或發生錯誤為止。  
  
 **TerminateProcessAfterTimeOut**  
 指出是否要在 **TimeOut** 選項指定的逾時期限之後，強制結束處理序。 只有在 **TimeOut** 不是 **0**時，才可以使用此選項。  
  
 **WindowStyle**  
 指定用來執行處理序的視窗樣式。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [運算式頁面](expressions/expressions-page.md)  
  
  
