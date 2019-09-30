---
title: 開發特定類型的指令碼元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d98a0a0293114e1b701ecd90f4a7b1ab058b0aa4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296402"
---
# <a name="developing-specific-types-of-script-components"></a>開發特定類型的指令碼元件

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  指令碼元件是您可以在封裝的資料流程中使用的可設定工具，幾乎可滿足 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所含的來源、轉換和目的地未能達成的任何需求。 本章節包含指令碼元件程式碼範例，以示範設定指令碼元件的四種選項：  
  
-   做為來源。  
  
-   做為具有同步輸出的轉換。  
  
-   做為具有非同步輸出的轉換。  
  
-   做為目的地。  
  
 如需指令碼元件的其他範例，請參閱[其他指令碼元件範例](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [以指令碼元件建立來源](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)  
 說明和示範如何使用指令碼元件建立資料流程來源。  
  
 [使用指令碼元件建立同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 說明和示範如何使用指令碼元件建立具有同步輸出的資料流程轉換。 這種轉換會在資料列通過元件時就地修改資料列。  
  
 [使用指令碼元件建立非同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 說明和示範如何使用指令碼元件建立具有非同步輸出的資料流程轉換。 這種轉換必須先讀取所有的資料列，才可以將更多的資訊 (例如，計算的彙總) 加入通過元件的資料。  
  
 [使用指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 說明和示範如何使用指令碼元件建立資料流程目的地。  
  
## <a name="see-also"></a>另請參閱  
 [比較指令碼解決方案和自訂物件](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [開發特定類型的資料流程元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  
