---
title: "傳回從指令碼工作的結果 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], status information
- ExecutionValue property
- status information [Integration Services]
- TaskResult property
- SSIS Script task, status information
ms.assetid: ac06805b-c2db-44bd-af5c-5a0debe36dd7
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dd3772ed20abbc594d171ea83a2f330d44a5be85
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="returning-results-from-the-script-task"></a>從指令碼工作中傳回結果
  指令碼工作使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> 與選擇性的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 屬性，將狀態資訊傳回 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 執行階段，可用以判斷在完成指令碼工作之後的工作流程路徑。  
  
## <a name="taskresult"></a>TaskResult  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> 屬性會報告工作是否已成功或失敗。 例如：  
  
 `Dts.TaskResult = ScriptResults.Success`  
  
## <a name="executionvalue"></a>ExecutionValue  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 屬性會選擇性地傳回使用者定義的物件，以量化或提供有關指令碼工作的成功或失敗的詳細資訊。 例如，FTP 工作使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 屬性傳回傳送的檔案數目。 執行 SQL 工作會傳回工作影響的資料列數。 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 也可用以判斷工作流程的路徑。 例如：  
  
 `Dim rowsAffected as Integer`  
  
 `...`  
  
 `rowsAffected = 1000`  
  
 `Dts.ExecutionValue = rowsAffected`  

