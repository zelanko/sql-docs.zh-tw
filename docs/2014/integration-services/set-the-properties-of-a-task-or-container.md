---
title: 設定工作或容器的屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], properties
ms.assetid: 52d47ca4-fb8c-493d-8b2b-48bb269f859b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 341ada76e65676050f9034df65f7a5f28284a3a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62878288"
---
# <a name="set-the-properties-of-a-task-or-container"></a>設定工作或容器的屬性
  您可以使用 [屬性] 視窗來設定工作和容器的大部分屬性。 例外的是工作集合的屬性，以及因太複雜而無法使用 [屬性] 視窗設定的屬性。 例如，您無法在 [屬性] 視窗中設定「Foreach 迴圈」容器所使用的列舉值。 您必須使用工作或容器編輯器來設定這些複雜屬性。 大部分工作和容器編輯器都具有多個節點，而且每個節點都包含相關的屬性。 節點的名稱表示此節點所包含之屬性的主旨。  
  
 下列程序將描述如何使用 [屬性] 視窗或對應的工作或容器編輯器來設定工作或容器的屬性。  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-the-properties-window"></a>使用屬性視窗來設定工作或容器的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  在 [控制流程] 索引標籤的設計介面上，以滑鼠右鍵按一下工作或容器，然後按一下 [屬性]。  
  
5.  在 [屬性] 視窗中更新屬性值。  
  
    > [!NOTE]  
    >  大部分的屬性都可以經由直接在文字方塊中輸入某個值，或從清單中選取某個值予以設定。 不過，有些屬性比較複雜，並具有自訂屬性編輯器。 若要設定這種屬性，請按一下文字方塊，然後按一下建立 ([...]) 按鈕開啟自訂編輯器。  
  
6.  (選擇性) 建立屬性運算式，以動態方式更新工作或容器的屬性。 如需詳細資訊，請參閱 [加入或變更屬性運算式](expressions/add-or-change-a-property-expression.md)。  
  
7.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-a-task-or-container-editor"></a>使用工作或容器編輯器來設定工作或容器的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  在 [控制流程] 索引標籤的設計介面上，以滑鼠右鍵按一下工作或容器，然後按一下 [編輯] 開啟對應的工作或容器編輯器。  
  
     如需如何設定「For 迴圈」容器的資訊，請參閱[設定 For 迴圈容器](control-flow/for-loop-container.md)。  
  
     如需如何設定「Foreach 迴圈」容器的資訊，請參閱 [設定 Foreach 迴圈容器](control-flow/foreach-loop-container.md)。  
  
    > [!NOTE]  
    >  「時序」容器沒有任何自訂編輯器。  
  
5.  如果工作或容器編輯器具有多個節點，請按一下包含您要設定之屬性的節點。  
  
6.  (選擇性) 按一下 [運算式]，然後在 [運算式] 頁面上建立屬性運算式，以動態方式更新工作或容器的屬性。 如需詳細資訊，請參閱[加入或變更屬性運算式](expressions/add-or-change-a-property-expression.md)。  
  
7.  更新屬性值。  
  
8.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](control-flow/integration-services-tasks.md)   
 [Integration Services 容器](control-flow/integration-services-containers.md)  
  
  
