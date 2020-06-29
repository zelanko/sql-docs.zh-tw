---
title: 執行處理工作編輯器（處理頁面） |Microsoft Docs
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 51b06136ce1380f04f64bc079f5db41f3d851c8a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85429175"
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
 輸入包含可執行檔的資料夾路徑，或按一下瀏覽按鈕 **（...）** ，然後找出資料夾。  
  
 **StandardInputVariable**  
 選取變數以提供該進程的輸入，或按一下 \<**New variable...**> 以建立新的變數：  
  
 **相關主題：**  [加入變數](../../2014/integration-services/add-variable.md)  
  
 **StandardOutputVariable**  
 選取一個變數來捕捉進程的輸出，或按一下 \<**New variable...**> 以建立新的變數。  
  
 **StandardErrorVariable**  
 選取一個變數來捕獲處理器的錯誤輸出，或按一下 \<**New variable...**> 以建立新的變數。  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 指出如果處理序的結束碼和 **SuccessValue**中指定的值不同時，工作是否失敗。  
  
 **SuccessValue**  
 指定可執行檔要表示成功時將傳回的值。 依預設，此值設定為 **0**。  
  
 **限制**  
 指定處理序可以執行的秒數。 若值為 **0** ，表示不使用逾時值，則處理序會一直執行到完成或發生錯誤為止。  
  
 **TerminateProcessAfterTimeOut**  
 指出是否要在 **TimeOut** 選項指定的逾時期限之後，強制結束處理序。 只有在 **TimeOut** 不是 **0**時，才可以使用此選項。  
  
 **WindowStyle**  
 指定用來執行處理序的視窗樣式。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [運算式頁面](expressions/expressions-page.md)  
  
  
