---
title: 多個優先順序條件約束 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- multiple precedence constraints
- precedence executables [Integration Services]
- precedence constraints [Integration Services], multiple
- constrained executables [Integration Services]
ms.assetid: 71c53ead-3d19-4bc1-aafd-e5b32595b420
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d4a9dc0f4b40320533828e2b1ef9f5f4cdfab9c5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036150"
---
# <a name="multiple-precedence-constraints"></a>多個優先順序條件約束
  優先順序條件約束會連接兩個可執行檔：兩個工作、兩個容器，或一個工作和一個容器。 其稱為優先順序可執行檔與受條件約束的可執行檔。 條件約束可執行檔可包含多個優先順序條件約束。 如需詳細資訊，請參閱 [Precedence Constraints](control-flow/precedence-constraints.md)。  
  
 藉由群組條件約束來組裝複雜的條件約束案例，可讓您在封裝中實作複雜的控制流程。 例如，在下圖中，工作 D 連結到工作 A 所`Success`條件約束，工作 D 會連結到工作 B 由`Failure`條件約束，以及工作 D 連結到工作 C`Success`條件約束。 工作 D 與工作 A、工作 D 與工作 B，以及工作 D 與工作 C 之間的優先順序條件約束會參與邏輯 *and* 關聯性。 因此，工作 A 必須成功執行、工作 B 必須失敗，而且工作 C 必須成功執行，才可以執行工作 D。  
  
 ![優先順序條件約束所連結的工作](media/precedenceconstraints.gif "優先順序條件約束所連結的工作")  
  
## <a name="logicaland-property"></a>LogicalAnd 屬性  
 如果工作或容器具有多個條件約束，則 `LogicalAnd` 屬性會指定是只評估優先順序條件約束，還是同時評估其他條件約束。  
  
 您可以設定`LogicalAnd`屬性使用**優先順序條件約束編輯器**中[!INCLUDE[ssIS](../includes/ssis-md.md)]設計工具中，或在 [屬性] 視窗中，[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]提供。  
  
## <a name="related-tasks"></a>相關工作  
 [設定優先順序條件約束的屬性](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  