---
description: 時序容器
title: 時序容器 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sequencecontainer.f1
helpviewer_keywords:
- Sequence container
- grouping control flows
- containers [Integration Services], Sequence
- subset control flow [Integration Services]
ms.assetid: 7731f91e-b8b3-4d96-a0d9-73f568547cb3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7951c07be9159162c31572933a17e7af27fcc951
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "92192828"
---
# <a name="sequence-container"></a>時序容器

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  「時序」容器會定義屬於封裝控制流程子集的控制流程。 「時序」容器會將封裝納入多個不同的控制流程中，而各流程中包含在整個封裝控制流程內執行的一項或多項工作和容器。  
  
 除了其他容器外，「時序」容器也可包含多個工作。 將工作和容器加入「時序」容器與將它們加入封裝相似，不同之處在於，您要將工作和容器拖曳至「時序」容器而非封裝容器。 如果「時序」容器包含一個以上的工作或容器，則您可以如同在封裝中所做的一樣，使用優先順序條件約束來連接它們。 如需詳細資訊，請參閱 [優先順序條件約束](../../integration-services/control-flow/precedence-constraints.md)。  
  
 使用「時序」容器有多項益處：  
  
-   停用工作群組，以便將封裝偵錯的焦點放在封裝控制流程的子集上。  
  
-   在同一個位置藉由設定「時序」容器而非個別工作的屬性，來管理多項工作的屬性。  
  
     例如，您可以將「時序」容器的 **Disable** 屬性設定為 [True]，以停用「時序」容器中的所有工作和容器。  
  
-   提供一群相關工作和容器所使用變數的範圍。  
  
-   將許多工作分組，讓您可以利用收合和展開「時序」容器的方式，更輕鬆地管理工作。  
  
     您還可以建立工作群組，使用 [群組] 方塊摺疊和展開。 不過，[群組] 方塊是設計階段的功能，不具有屬性或執行階段的行為。 如需詳細資訊，請參閱 [將元件分組或取消分組](../../integration-services/group-or-ungroup-components.md)。  
  
-   設定「時序」容器的交易屬性，以定義封裝控制流程子集的異動。 使用這種方式，可以以更細微的層級管理交易。  
  
     例如，如果「時序」容器包括兩項相關的工作，其中一項工作為刪除資料表中的資料，而另一項工作會將資料插入資料表中，則可設定交易，以確認刪除動作會在插入動作失敗時回復。 如需詳細資訊，請參閱 [Integration Services 交易](../../integration-services/integration-services-transactions.md)。  
  
## <a name="configuration-of-the-sequence-container"></a>設定時序容器  
 「時序」容器沒有自訂使用者介面，而且您只能在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [屬性] 視窗中或利用撰寫程式的方式進行設定。  
  
 如需以程式設計方式設定這些屬性的詳細資訊，請參閱《開發人員指南》中 **T:Microsoft.SqlServer.Dts.Runtime.Sequence** 類別的文件。  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中元件屬性的資訊，請參閱 [設定工作或容器的屬性](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)。  
  
## <a name="see-also"></a>另請參閱  
 [在控制流程中加入或刪除工作或容器](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [使用預設的優先順序條件約束來連線工作和容器](./precedence-constraints.md)   
 [Integration Services 容器](../../integration-services/control-flow/integration-services-containers.md)  
  
