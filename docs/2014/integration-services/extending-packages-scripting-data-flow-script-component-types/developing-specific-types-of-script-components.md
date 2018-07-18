---
title: 開發特定類型的指令碼元件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 675b83beb96bda947e72852ee9a82772104088df
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37184615"
---
# <a name="developing-specific-types-of-script-components"></a>開發特定類型的指令碼元件
  指令碼元件是您可以在封裝的資料流程中使用的可設定工具，幾乎可滿足 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所含的來源、轉換和目的地未能達成的任何需求。 本章節包含指令碼元件程式碼範例，以示範設定指令碼元件的四種選項：  
  
-   做為來源。  
  
-   做為具有同步輸出的轉換。  
  
-   做為具有非同步輸出的轉換。  
  
-   做為目的地。  
  
 如需指令碼元件的其他範例，請參閱[其他指令碼元件範例](../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [以指令碼元件建立來源](creating-a-source-with-the-script-component.md)  
 說明和示範如何使用指令碼元件建立資料流程來源。  
  
 [使用指令碼元件建立同步轉換](creating-a-synchronous-transformation-with-the-script-component.md)  
 說明和示範如何使用指令碼元件建立具有同步輸出的資料流程轉換。 這種轉換會在資料列通過元件時就地修改資料列。  
  
 [使用指令碼元件建立非同步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 說明和示範如何使用指令碼元件建立具有非同步輸出的資料流程轉換。 這種轉換必須先讀取所有的資料列，才可以將更多的資訊 (例如，計算的彙總) 加入通過元件的資料。  
  
 [使用指令碼元件建立目的地](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 說明和示範如何使用指令碼元件建立資料流程目的地。  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期** <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [比較指令碼解決方案和自訂物件](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [開發特定類型的資料流程元件](../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  
