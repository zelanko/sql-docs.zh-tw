---
title: 設定 For 迴圈容器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: b9cd7ea7-b198-4a35-8b16-6acf09611ca5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2adcb3e79e3733b5fb8151bfa7f65e7bebb4d910
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126160"
---
# <a name="configure-a-for-loop-container"></a>設定 For 迴圈容器
  此程序描述如何使用 [For 迴圈編輯器] 對話方塊設定「For 迴圈」容器。  
  
 如需 For 迴圈容器的範例，請參閱 bimonkey.com 上的 [SSIS Loops that do not fail](http://go.microsoft.com/fwlink/?LinkId=240295)。  
  
### <a name="to-configure-the-for-loop-container"></a>設定 For 迴圈容器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，按兩下「For 迴圈」容器以開啟 [For 迴圈編輯器]。  
  
2.  (選擇性) 修改「For 迴圈」容器的名稱和描述。  
  
3.  (選擇性) 在 [InitExpression] 文字方塊中輸入初始化運算式。  
  
4.  在 [EvalExpression] 文字方塊中輸入評估運算式。  
  
    > [!NOTE]  
    >  運算式必須評估為布林。 如果運算式的評估為 `false`，迴圈將停止執行。  
  
5.  (選擇性) 在 [AssignExpression] 文字方塊中輸入指派運算式。  
  
6.  (選擇性) 按一下 [運算式]，然後在 [運算式] 頁面上建立「For 迴圈」容器之屬性的屬性運算式。 如需詳細資訊，請參閱[加入或變更屬性運算式](expressions/add-or-change-a-property-expression.md)。  
  
7.  按一下 [確定]，以關閉 [For 迴圈編輯器]。  
  
## <a name="see-also"></a>另請參閱  
 [For 迴圈容器](control-flow/for-loop-container.md)   
 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)   
 [在套件中使用屬性運算式](expressions/use-property-expressions-in-packages.md)  
  
  
