---
title: 使用轉換來轉換資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], transformations
- transformations [Integration Services], about transformations
- transforming data [Integration Services]
ms.assetid: e1340b6f-ef75-4b14-af6f-823586eff0ed
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9fb4014688f1899e813d1df3e677caf9ad7bfbf1
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382036"
---
# <a name="transform-data-with-transformations"></a>使用轉換來轉換資料
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含三種類型的資料流程元件：來源、轉換與目的地。  
  
 下圖顯示包含一個來源、兩個轉換及一個目的地的簡單資料流程。  
  
 ![Data flow](../../media/mw-dts-08.gif "Data flow")  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 轉換提供下列功能：  
  
-   分割、複製以及合併資料列集，並執行查閱作業。  
  
-   透過套用轉換，例如變更小寫為大寫，來更新資料行值及新建資料行。  
  
-   執行商業智慧作業，例如清除資料、採礦文字或執行資料採礦預測查詢等。  
  
-   新建包含彙總值或排序值、範例資料或樞紐和取消樞紐資料的資料列集。  
  
-   執行例如匯出和匯入資料、提供稽核資訊以及使用緩時變維度等工作。  
  
 如需詳細資訊，請參閱 [Integration Services 轉換](integration-services-transformations.md)。  
  
 您也可以撰寫自訂轉換。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 和 [開發特定類型的資料流程元件](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)。  
  
 在將轉換加入資料流程設計師之後，設定轉換之前，您可以透過將資料流程中另一轉換或來源的輸出連接到轉換的輸入，以將此轉換連接到資料流程。 兩個資料流程元件之間的連接子稱為路徑。 如需連接元件以及使用路徑的詳細資訊，請參閱 [以路徑連接元件](../../connect-components-with-paths.md)。  
  
### <a name="to-add-a-transformation-to-a-data-flow"></a>將轉換加入資料流程  
  
-   [在資料流程中加入或刪除元件](../add-or-delete-a-component-in-a-data-flow.md)  
  
### <a name="to-connect-a-transformation-to-a-data-flow"></a>將轉換連接到資料流程  
  
-   [連接資料流程中的元件](../connect-components-in-a-data-flow.md)  
  
### <a name="to-set-the-properties-of-a-transformation"></a>設定轉換的屬性  
  
-   [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料流程工作](../../control-flow/data-flow-task.md)   
 [資料流程](../data-flow.md)   
 [以路徑連接元件](../../connect-components-with-paths.md)   
 [資料中的錯誤處理](../error-handling-in-data.md)   
 [資料流程](../data-flow.md)  
  
  
