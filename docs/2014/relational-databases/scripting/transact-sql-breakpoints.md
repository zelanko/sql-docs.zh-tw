---
title: Transact-SQL 中斷點
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoints
ms.assetid: c234430f-bd94-4d0d-9e74-2bf11681fa50
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b5d363e7f68ba735168ef17eeff8e9605c54b2f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068453"
---
# <a name="transact-sql-breakpoints"></a>Transact-SQL 中斷點
  中斷點指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具要在特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式上暫停執行，然後您就可以在該點檢視程式碼元素的狀態。  
  
## <a name="breakpoints"></a>中斷點  
 執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具時，您可以切換特定陳述式上的中斷點。 執行到具有中斷點的陳述式時，偵錯工具會暫停執行，讓您可以檢視偵錯資訊，例如變數和參數中的值。  
  
 您可以在編輯器視窗中個別管理中斷點，或是使用 [中斷點]  視窗統一進行管理。 您可以編輯中斷點以指定項目，例如應該暫停執行的特定條件，或要在執行中斷點時採取的動作。  
  
## <a name="breakpoint-tasks"></a>中斷點工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何指定您要暫停偵錯工具的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。|[切換中斷點](../spatial/point.md)|  
|描述如何暫時停用中斷點，稍後再重新予以啟用。 同時描述如何刪除中斷點。|[啟用、停用以及刪除中斷點](enable-disable-and-delete-breakpoints.md)|  
|描述如何指定條件，而條件定義是否依據所指定 Transact-SQL 運算式的評估結果來中斷中斷點。|[指定中斷點條件](specify-a-breakpoint-condition.md)|  
|描述如何指定叫用計數，而叫用計數只有在包含中斷點的陳述式已經執行指定的次數時才會導致中斷點中斷。|[指定叫用計數](specify-a-hit-count.md)|  
|描述如何指定篩選，而篩選只會中斷所指定處理序或執行緒的中斷點。|[指定中斷點篩選條件](specify-a-breakpoint-filter.md)|  
|描述如何指定 [叫用時]  動作，而此動作是在執行中斷點陳述式時執行的自訂作業。 範例為列印訊息。|[指定中斷點動作](specify-a-breakpoint-action.md)|  
|描述如何編輯中斷點的位置。|[編輯中斷點位置](edit-a-breakpoint-location.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 偵錯工具資訊](transact-sql-debugger-information.md)  
  
  
