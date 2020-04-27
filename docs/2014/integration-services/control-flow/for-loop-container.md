---
title: For 迴圈容器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.forloopcontainerdetails.f1
helpviewer_keywords:
- repeating control flow
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: 44cf7355-992b-4bbf-a28c-bfb012de06f6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 991223c373113b465c3182f552e5f5d157efef9f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62831600"
---
# <a name="for-loop-container"></a>For 迴圈容器
  「For 迴圈」容器定義封裝中重複的控制流程。 迴圈實作與程式設計語言中 **For** 迴圈的結構類似。 在每次迴圈重複中，「For 迴圈」容器都會評估運算式並重複其工作流程，直到運算式評估為 `False` 為止。  
  
 「For 迴圈」容器使用下列元素定義迴圈：  
  
-   選擇性初始化運算式，會指派值給迴圈計數器。  
  
-   評估運算式，其中含有用來測試迴圈應停止或繼續的運算式。  
  
-   選擇性反覆運算的運算式，會累加或遞減迴圈計數器。  
  
 下列圖表顯示含有傳送郵件工作的「For 迴圈」容器。 如果初始化運算式為 `@Counter = 0`、評估運算式為 `@Counter < 4`，且反覆運算的運算式為 `@Counter = @Counter + 1`，則迴圈會重複四次並傳送四則電子郵件訊息。  
  
 ![For 迴圈容器會重複工作四次](../media/ssis-forloop.gif "For 迴圈容器會重複工作四次")  
  
 運算式必須是有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 運算式。  
  
 若要建立初始化和指派運算式，可使用指派運算子 (=)。 除了「For 迴圈」容器中的初始化和指派運算式類型可使用此運算子外，Integration Services 運算式文法不另外支援此運算子。 任何使用指派運算子的運算式都必須使用此語法 `@Var = <expression>`，其中 **Var** 是執行階段變數，而 \<運算式> 是遵循 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 運算式語法規則的運算式。 運算式可包含變數、常值，以及任何 SSIS 運算式文法支援的運算子和函數。 運算式必須評估為可轉換成變數資料類型的資料類型。  
  
 「For 迴圈」容器只能有一個評估運算式。 這表示「For 迴圈」容器執行其所有控制流程元素的次數皆相同。 由於「For 迴圈」容器可包含其他「For 迴圈」容器，因此您可以在封裝中建立巢狀迴圈並實作複雜的迴圈。  
  
 您可以在「For 迴圈」容器上設定交易屬性，用來定義封裝控制流程子集的交易。 使用這種方式，可以以更細微的層級管理交易。 例如，如果「For 迴圈」容器多次重複更新資料表中資料的控制流程，您可設定讓「For 迴圈」容器及其控制流程使用交易，以確保若非所有資料都成功更新，則不更新任何資料。 如需詳細資訊，請參閱 [Integration Services 交易](../integration-services-transactions.md)。  
  
## <a name="configuration-of-the-for-loop-container"></a>設定 For 迴圈容器  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [For 迴圈編輯器](../for-loop-editor.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請參閱《開發人員指南》中 **T:Microsoft.SqlServer.Dts.Runtime.ForLoop** 類別的文件。  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何設定「For 迴圈」容器的詳細資訊，請參閱下列主題。  
  
-   [設定 For 迴圈容器](for-loop-container.md)  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>另請參閱  
 [控制流程](control-flow.md)   
 [Integration Services &#40;SSIS&#41; 運算式](../expressions/integration-services-ssis-expressions.md)  
  
  
