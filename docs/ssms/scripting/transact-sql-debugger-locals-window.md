---
title: 本機視窗
description: 了解如何使用 Transact-SQL 偵錯工具的 [區域變數] 視窗，以顯示及修改目前呼叫堆疊框架中的運算式。
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 00c6704418210c0913470688ae4c8d7a55facaf4
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243738"
---
# <a name="transact-sql-debugger---locals-window"></a>Transact-SQL 偵錯工具 - 區域變數視窗

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[區域變數] 視窗會顯示有關 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具目前範圍中之區域運算式的資訊。 此範圍會設定為 [呼叫堆疊] 視窗內選取的目前呼叫堆疊框架。 您必須在偵錯模式中，才能顯示本機運算式。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>工作清單

**存取區域變數視窗**
  
-   在 [偵錯] 功能表中，按一下 [視窗]，然後按一下 [區域變數]。  
  
 **變更運算式的值**  
  
-   以滑鼠右鍵按一下運算式，然後選取 [編輯值]。  
  
## <a name="columns"></a>資料行  
 **名稱**  
 為本機運算式的名稱。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具會列出名稱以 @@ 開頭的變數、參數和系統函式。  
  
 **ReplTest1**  
 顯示目前指派給本機運算式的值。 當沒有任何值指派給運算式時，此資料行會是空白的。  
  
 如果運算式的長度超過 **[值]** 資料行的寬度，當您將指標放在該運算式的 **[值]** 資料格上方時，工具提示會顯示完整的值。  
  
 **[值]** 資料格內的放大鏡圖示表示可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具視覺化檢視。 在此清單中，您可以指定 **[文字視覺化檢視]** 、 **[XML 視覺化檢視]** 或 **[HTML 視覺化檢視]** 。 若要啟動偵錯工具視覺化檢視，請按一下放大鏡圖示。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具會開啟一個對話方塊，其中會以對資料類型適合的格式顯示資料。  
  
 **型別**  
 顯示此運算式的資料類型。  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 偵錯工具](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 偵錯工具資訊](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [監看式視窗](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [呼叫堆疊視窗](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [快速監看式對話方塊](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
