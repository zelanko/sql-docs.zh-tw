---
description: 使用轉換來轉換資料
title: 使用轉換來轉換資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], transformations
- transformations [Integration Services], about transformations
- transforming data [Integration Services]
ms.assetid: e1340b6f-ef75-4b14-af6f-823586eff0ed
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2d9422574f80febefc6458b389f04b4b1625b22c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425650"
---
# <a name="transform-data-with-transformations"></a>使用轉換來轉換資料

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含三種類型的資料流程元件：來源、轉換與目的地。  
  
 下圖顯示包含一個來源、兩個轉換及一個目的地的簡單資料流程。  
  
 ![](../../../integration-services/data-flow/media/mw-dts-08.gif "設計師中")  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 轉換提供下列功能：  
  
-   分割、複製以及合併資料列集，並執行查閱作業。  
  
-   透過套用轉換，例如變更小寫為大寫，來更新資料行值及新建資料行。  
  
-   執行商業智慧作業，例如清除資料、採礦文字或執行資料採礦預測查詢等。  
  
-   新建包含彙總值或排序值、範例資料或樞紐和取消樞紐資料的資料列集。  
  
-   執行例如匯出和匯入資料、提供稽核資訊以及使用緩時變維度等工作。  
  
 如需詳細資訊，請參閱 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)。  
  
 您也可以撰寫自訂轉換。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 和 [開發特定類型的資料流程元件](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)。  
  
 在將轉換加入資料流程設計師之後，設定轉換之前，您可以透過將資料流程中另一轉換或來源的輸出連接到轉換的輸入，以將此轉換連接到資料流程。 兩個資料流程元件之間的連接子稱為路徑。 如需連接元件以及使用路徑的詳細資訊，請參閱 [以路徑連接元件](https://msdn.microsoft.com/library/05633e4c-1370-4b05-802b-f36b07dd71c8)。  
  
### <a name="to-add-a-transformation-to-a-data-flow"></a>將轉換加入資料流程  
  
-   [在資料流程中加入或刪除元件](../../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
### <a name="to-connect-a-transformation-to-a-data-flow"></a>將轉換連接到資料流程  
  
-   [連接資料流程中的元件](../../../integration-services/data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-set-the-properties-of-a-transformation"></a>設定轉換的屬性  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料流程工作](../../../integration-services/control-flow/data-flow-task.md)   
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [以路徑連接元件](https://msdn.microsoft.com/library/05633e4c-1370-4b05-802b-f36b07dd71c8)   
 [資料中的錯誤處理](../../../integration-services/data-flow/error-handling-in-data.md)   
 [資料流程](../../../integration-services/data-flow/data-flow.md)  
  
  
