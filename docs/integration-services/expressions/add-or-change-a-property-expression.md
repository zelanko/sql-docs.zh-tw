---
title: 加入或變更屬性運算式 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], creating
- expressions [Integration Services], property expressions
ms.assetid: cb5da499-065f-4fa6-9f6d-5bc5f385241e
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 423942773422452cc6b46b808fbe53a61270db2f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="add-or-change-a-property-expression"></a>加入或變更屬性運算式
  您可以為封裝、工作、「Foreach 迴圈」容器、「For 迴圈」容器、「時序」容器、事件處理常式、封裝和專案層級的連接管理員和記錄提供者建立屬性運算式。  
  
 若要建立或變更屬性運算式，您可以使用 [屬性運算式編輯器] 或 [運算式產生器]。 您可以從適用於工作的自訂編輯器或 [屬性] 視窗存取 [屬性運算式編輯器]。 您可以從 [屬性運算式編輯器] 內部存取 [運算式產生器]。 雖然您可以在 [屬性運算式編輯器] 或 [運算式產生器] 中撰寫運算式，但是 [運算式產生器] 會提供一組圖形工具，讓您輕鬆地建立複雜運算式。  
  
 如需深入了解 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的語法、運算子和函數，請參閱[運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md) 和[函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)。 每個運算子或函數的主題都包含了在運算式中使用該運算子或函數的範例。 如需更複雜之運算式的相關範例，請參閱 [在封裝中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)。  
  
### <a name="to-create-or-change-a-property-expression"></a>建立或變更屬性運算式  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟，然後執行下列其中之一：  
  
    -   如果項目是工作或容器，請按兩下該項目，然後按一下編輯器中的 [運算式]。  
  
    -   以滑鼠右鍵按一下項目，然後按一下 [屬性]。  
  
3.  在 [運算式] 方塊中按一下，然後按一下省略符號 [(…)]。  
  
4.  在 [屬性運算式編輯器] 中，選取 [屬性] 清單中的屬性，然後執行下列其中之一：  
  
    -   直接在 [運算式] 資料行中輸入或變更屬性運算式，然後按一下 [確定]。  
  
         – 或 –  
  
    -   在屬性的運算式資料列中，按一下省略符號 (…) 開啟 [運算式產生器]。  
  
5.  (選擇性) 在 [運算式產生器] 中，進行下列任何一項工作：  
  
    -   若要存取系統和使用者定義的變數，請展開 [變數]。  
  
    -   若要存取 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 運算式語言所提供的函數、轉換和運算子，請展開 [數學函數]、[字串函數]、[日期/時間函數]、[NULL 函數]、[類型轉換] 和 [運算子]。  
  
    -   若要在 [運算式產生器] 中建立或變更運算式，請將變數、資料行、函數、運算子和轉換拖曳至 [運算式] 方塊，或者直接在方塊中輸入運算式。  
  
    -   若要檢視運算式的評估結果，請在 [運算式產生器] 中按一下 [評估運算式]。  
  
         如果運算式無效，則會出現警示，描述運算式中的語法錯誤。  
  
        > [!NOTE]  
        >  評估運算式不會將評估結果指派給屬性。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)   
 [在封裝中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)   
 [Integration Services &#40;SSIS&#41; 封裝](../../integration-services/integration-services-ssis-packages.md)   
 [Integration Services 容器](../../integration-services/control-flow/integration-services-containers.md)   
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services &#40;SSIS&#41; 事件處理常式](../../integration-services/integration-services-ssis-event-handlers.md)   
 [Integration Services &#40;SSIS&#41; 連線](../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
