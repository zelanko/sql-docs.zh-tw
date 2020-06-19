---
title: Analysis Services 處理工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asprocessingtask.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: efb7193eb79624a483fc728cf80308c4b6e1c959
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920223"
---
# <a name="analysis-services-processing-task"></a>Analysis Services 處理工作
  「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理」工作會處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件，例如表格式模型、Cube、維度及採礦模型。  
  
 處理表格式模型時，請牢記以下事項：  
  
-   您無法在表格式模型上執行影響分析。  
  
-   系統不會公開表格式模型的部分處理選項，例如 [處理重組] 和 [處理重新計算]。 您可以使用「執行 DLL」工作，執行這些功能。  
  
-   [處理索引] 和 [處理更新] 選項不適合表格式模型，因此應該不會使用。  
  
-   表格式模型會忽略批次處理設定。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括多項執行商業智慧作業的工作，例如執行「資料定義語言」(Data Definition Language，DDL) 和執行資料採礦預測查詢。 如需有關相關之商業智慧工作的詳細資訊，請按下列其中一個主題：  
  
-   [Analysis Services 執行 DDL 工作](analysis-services-execute-ddl-task.md)  
  
-   [資料採礦查詢工作](data-mining-query-task.md)  
  
## <a name="object-processing"></a>物件處理  
 可以同時處理多個物件。 處理多個物件時，您會定義套用至處理該批次中所有物件的設定。  
  
 批次中的物件可循序或平行處理。 如果批次未包含重視處理順序的物件，使用平行處理可加快處理速度。 如果平行處理批次中的物件，可設定讓工作判斷平行處理的物件數目，或者手動指定同時處理的物件數目。 如果循序處理物件，可將所有物件列入一項交易中，或針對批次中各物件使用不同的交易，藉此在批次上設定交易屬性。  
  
 當您處理分析物件時，可能也會想處理倚賴該些物件的物件。 「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理」工作包含的選項除了可以處理選取的物件以外，也可以處理任何相依物件。  
  
 您通常會在處理事實資料表之前處理維度資料表。 如果嘗試在處理維度資料表之前處理事實資料表，則可能會出現錯誤。  
  
 此工作亦可讓您設定在維度索引鍵中處理錯誤。 例如，工作可忽略錯誤，或在發生指定的錯誤數目之後停止。 工作可使用預設錯誤組態，或者您可以建構自訂錯誤組態。 在自訂錯誤組態中，請指定工作處理錯誤的方式和錯誤的條件。 例如，您可以指定在發生四項錯誤時停止執行工作，或指定工作處理 **Null** 索引鍵值的方式。 自訂錯誤組態亦可包含錯誤記錄的路徑。  
  
> [!NOTE]  
>  「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理」工作只能處理使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具建立的分析物件。  
  
 此工作經常用來搭配將資料載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的「大量插入」工作使用，或搭配實作將資料載入資料表之資料流程的資料流程工作使用。 例如，資料流程工作可能包含從線上交易處理 (OLTP) 資料庫擷取資料，並將資料載入資料倉儲中事實資料表的資料流程，而在此之後，會呼叫「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理」工作處理於資料倉儲上建立的 Cube。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理工作會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員來連線到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)。  
  
## <a name="error-handling"></a>錯誤處理  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Analysis Services 處理工作的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Analysis Services 處理工作編輯器 &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Analysis Services 處理工作編輯器 &#40;Analysis Services 頁面&#41;](../analysis-services-processing-task-editor-analysis-services-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>以程式設計方式設定 Analysis Services 處理工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列其中一個主題：  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
  
