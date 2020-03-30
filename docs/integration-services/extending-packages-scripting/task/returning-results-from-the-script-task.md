---
title: 從指令碼工作傳回結果 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], status information
- ExecutionValue property
- status information [Integration Services]
- TaskResult property
- SSIS Script task, status information
ms.assetid: ac06805b-c2db-44bd-af5c-5a0debe36dd7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0c5fa5e546f566362b76691ffc2e316d0ff6a485
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296388"
---
# <a name="returning-results-from-the-script-task"></a>從指令碼工作中傳回結果

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
