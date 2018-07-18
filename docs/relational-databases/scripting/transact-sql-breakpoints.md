---
title: Transact-SQL 中斷點 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoints
ms.assetid: c234430f-bd94-4d0d-9e74-2bf11681fa50
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7c60dcd710dcb8ac80b501175f7ac2478b4fce4e
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34333419"
---
# <a name="transact-sql-breakpoints"></a>Transact-SQL 中斷點
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  中斷點指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具要在特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式上暫停執行，然後您就可以在該點檢視程式碼元素的狀態。  
  
## <a name="breakpoints"></a>中斷點  
 執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具時，您可以切換特定陳述式上的中斷點。 執行到具有中斷點的陳述式時，偵錯工具會暫停執行，讓您可以檢視偵錯資訊，例如變數和參數中的值。  
  
 您可以在編輯器視窗中個別管理中斷點，或是使用 [中斷點] 視窗統一進行管理。 您可以編輯中斷點以指定項目，例如應該暫停執行的特定條件，或要在執行中斷點時採取的動作。  
  
## <a name="breakpoint-tasks"></a>中斷點工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何指定您要暫停偵錯工具的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。|[切換中斷點](../../relational-databases/scripting/toggle-a-breakpoint.md)|  
|描述如何暫時停用中斷點，稍後再重新予以啟用。 同時描述如何刪除中斷點。|[啟用、停用以及刪除中斷點](../../relational-databases/scripting/enable-disable-and-delete-breakpoints.md)|  
|描述如何指定條件，而條件定義是否依據所指定 Transact-SQL 運算式的評估結果來中斷中斷點。|[指定中斷點條件](../../relational-databases/scripting/specify-a-breakpoint-condition.md)|  
|描述如何指定叫用計數，而叫用計數只有在包含中斷點的陳述式已經執行指定的次數時才會導致中斷點中斷。|[指定叫用計數](../../relational-databases/scripting/specify-a-hit-count.md)|  
|描述如何指定篩選，而篩選只會中斷所指定處理序或執行緒的中斷點。|[指定中斷點篩選條件](../../relational-databases/scripting/specify-a-breakpoint-filter.md)|  
|描述如何指定 [叫用時] 動作，而此動作是在執行中斷點陳述式時執行的自訂作業。 範例為列印訊息。|[指定中斷點動作](../../relational-databases/scripting/specify-a-breakpoint-action.md)|  
|描述如何編輯中斷點的位置。|[編輯中斷點位置](../../relational-databases/scripting/edit-a-breakpoint-location.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 偵錯工具資訊](../../relational-databases/scripting/transact-sql-debugger-information.md)  
  
  
