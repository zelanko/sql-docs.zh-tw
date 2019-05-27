---
title: 參數化對話方塊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.parameter.f1
ms.assetid: fac02b6d-d247-447a-8940-e8700c7ac350
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7d60820ba7c384347aeeec80d8c41f934078eca8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056866"
---
# <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
  [參數化] 對話方塊可讓您將新的或現有的參數與工作屬性產生關聯。 您可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，以滑鼠右鍵按一下工作或 [控制流程] 索引標籤，然後按一下 [參數化] 即可開啟此對話方塊。 下列清單描述對話方塊中的 UI 元素。 如需參數的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 參數](integration-services-ssis-package-and-project-parameters.md)。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **屬性**  
 選取要與參數產生關聯的工作屬性。 此清單會以可參數化的所有屬性擴展。  
  
 **使用現有的參數**  
 選取此選項可讓任務屬性與某個現有的參數產生關聯，然後從下拉式清單中選取該參數。  
  
 **不使用參數**  
 選取此選項以移除參數的參考。 未刪除參數。  
  
 **建立新的參數**  
 選取此選項可建立要與任務屬性產生關聯的新參數。  
  
 **名稱**  
 指定您要建立之參數的名稱。  
  
 **說明**  
 指定參數的描述。  
  
 **值**  
 指定參數的預設值。 這也稱作設計預設值，以後在部署時可以覆蓋該值。  
  
 **範圍**  
 選取 [專案] 或 [封裝] 選項來指定參數的範圍。 專案參數可用於向專案中的一個或多個封裝提供專案接收的任何外部輸入。 封裝參數可讓您修改封裝執行，而不需要編輯和重新部署封裝。  
  
 **區分**  
 透過檢查或清除該核取方塊來指定參數是否敏感。 敏感性參數值會在目錄中加密，以 Transact-SQL 或 SQL Server Management Studio 來檢視時，會顯示為 NULL 值。  
  
 **必要**  
 指定參數是否是否需要先指定一個值 (非設計預設值)，指定的封裝才能執行。  
  
## <a name="uielement-list"></a>UIElement 清單  
  
