---
title: 指定中斷點條件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint conditions
ms.assetid: b43d8a2b-99a3-4fb7-8848-99c042ea7ef7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e331c8dfd533a99d2938633fe7dae5654f5c0ce3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063735"
---
# <a name="specify-a-breakpoint-condition"></a>指定中斷點條件
  中斷點條件是指偵錯工具在到達中斷點時所評估的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 運算式。 如果已滿足條件，而且到達任何指定的叫用次數，偵錯工具就會中斷或執行為中斷點指定的動作。  
  
## <a name="specifying-conditions"></a>指定條件  
 指定的運算式必須是評估為布林值的有效 Transact-SQL 運算式。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/expressions-transact-sql)。  
  
 如果您指定了具有無效語法的中斷點條件，就會立即顯示警告訊息。 如果您指定了具有有效語法但無效語意的條件，就會在第一次叫用中斷點時顯示警告訊息。 在任何一種情況中，偵錯工具都會在叫用無效的中斷點時中斷執行。  
  
#### <a name="to-specify-a-condition"></a>若要指定條件  
  
1.  在編輯器視窗中，以滑鼠右鍵按一下中斷點圖像，然後按一下快速鍵功能表上的 [條件]。  
  
     -或-  
  
     在 [中斷點] 視窗中，以滑鼠右鍵按一下中斷點圖像，然後按一下快速鍵功能表上的 [條件]。  
  
2.  在 [中斷點條件] 對話方塊的 [條件] 方塊中，輸入有效的布林值運算式。  
  
3.  選擇**成立**如果您想要在運算式評估為時中斷`true`，或選擇**已變更**如果您想要變更運算式的值時中斷。  
  
    > [!NOTE]  
    >  在第一次到達中斷點之前，偵錯工具不會評估布林運算式。 如果您選擇 [已變更]，偵錯工具不會將第一次評估視為變更，因此偵錯工具不會在第一次評估時中斷。  
  
## <a name="see-also"></a>另請參閱  
 [指定叫用計數](specify-a-hit-count.md)   
 [指定中斷點動作](specify-a-breakpoint-action.md)  
