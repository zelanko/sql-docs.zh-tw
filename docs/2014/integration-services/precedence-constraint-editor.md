---
title: 優先順序條件約束編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.precedenceconstraint.f1
helpviewer_keywords:
- Precedence Constraint Editor dialog box
ms.assetid: b10d4330-6e35-4037-b309-ef56efcd60c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 639436ec39301189ae172ce9cb7f58ea96c9cc11
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388306"
---
# <a name="precedence-constraint-editor"></a>優先順序條件約束編輯器
  使用 **[優先順序條件約束編輯器]** 對話方塊，即可設定優先順序條件約束。  
  
## <a name="options"></a>選項。  
 **評估作業**  
 指定優先順序條件約束所使用的評估作業。 作業為：**條件約束**，**運算式**，**運算式與條件約束**，和**運算式或條件約束**。  
  
 **值**  
 指定的條件約束值：**成功**，**失敗**，或**完成**。  
  
> [!NOTE]  
>  優先順序條件約束線條若是綠色代表 [成功]，反白顯示代表 [失敗]，而藍色代表 [完成]。  
  
 **運算式**  
 如果使用 [運算式]、[運算式與條件約束] 或 [運算式或條件約束] 作業，請輸入運算式或啟動運算式產生器以建立運算式。 運算式必須評估為布林。  
  
 **測試**  
 驗證運算式。  
  
 **邏輯 AND**  
 選取即可指定同一個可執行檔上的多個優先順序條件約束必須一起評估。 所有運算式都必須評估為 `True`。  
  
> [!NOTE]  
>  此種類型的優先順序條件約束會顯示為綠色、反白顯示或藍色的實線。  
  
 **邏輯 OR**  
 選取即可指定同一個可執行檔上的多個優先順序條件約束必須一起評估。 必須至少有一個條件約束評估為 `True`。  
  
> [!NOTE]  
>  此種類型的優先順序條件約束會顯示為綠色、反白顯示或藍色的虛線。  
  
## <a name="see-also"></a>另請參閱  
 [優先順序條件約束](control-flow/precedence-constraints.md)   
 [Integration Services 工作](control-flow/integration-services-tasks.md)   
 [Integration Services 容器](control-flow/integration-services-containers.md)   
 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)  
  
  
