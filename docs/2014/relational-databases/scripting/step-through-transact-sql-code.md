---
title: 逐步執行 Transact-SQL 程式碼
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, debugging code
- Transact-SQL debugger, step over
- Transact-SQL debugger, step out
- Transact-SQL debugger, step into
ms.assetid: e09079b8-c4c9-42b4-821b-4ce81a98a086
author: rothja
ms.author: jroth
ms.openlocfilehash: aa60ae2e275646812c226bd2fd9cd945174bab54
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068465"
---
# <a name="step-through-transact-sql-code"></a>逐步執行 Transact-SQL 程式碼
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具可讓您控制哪些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式要在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器視窗中執行。 您可以在個別的陳述式上暫停偵錯工具，然後在該點檢視程式碼項目的狀態。  
  
## <a name="breakpoints"></a>中斷點  
 中斷點會告知偵錯工具要在特定的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式上暫停執行作業。 如需有關中斷點的詳細資訊，請參閱＜使用 Transact-SQL 中斷點＞。  
  
## <a name="controlling-statement-execution"></a>控制陳述式執行  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具中，您可以指定下列選項，以便在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼中從目前的陳述式執行：  
  
-   執行到下一個中斷點。  
  
-   逐步執行下一個陳述式。  
  
     如果下一個陳述式會叫用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序、函數或觸發程序，偵錯工具就會顯示包含模組程式碼的新 [查詢編輯器] 視窗。 此視窗會處於偵錯模式中，而且執行作業會在模組的第一個陳述式上暫停。 接著，您就可以透過設定中斷點或逐步執行程式碼，在模組程式碼之間移動。  
  
-   不進入下一個陳述式。  
  
     系統會執行下一個陳述式。 不過，如果此陳述式會叫用預存程序、函數或觸發程序，模組程式碼就會執行直到完成為止，而且結果會傳回給呼叫的程式碼。 如果您確定預存程序沒有任何錯誤，就可以不進入此預存程序。 執行作業會在呼叫預存程序、函數或觸發程序之後的陳述式上暫停。  
  
-   跳離預存程序、函數或觸發程序。  
  
     執行作業會在呼叫預存程序、函數或觸發程序之後的陳述式上暫停。  
  
-   從目前的位置執行到指標的目前位置，並且忽略所有中斷點。  
  
 下表將列出您可以控制陳述式如何在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具中執行的各種方式。  
  
|動作|程序|  
|------------|---------------|  
|執行所有陳述式，從目前的陳述式到下一個端點|在 [偵錯]**** 功能表上按一下 [繼續]****。<br /><br /> 在 [**調試**] 工具列上，按一下 [**繼續**] 按鈕。|  
|逐步執行下一個陳述式或模組|在 [**調試**] 功能表上，按一下 [**逐步**執行]。<br /><br /> 在 [**調試**] 工具列上，按一下 [**逐步**執行] 按鈕。<br /><br /> 按下 F11。|  
|不進入下一個陳述式或模組|按一下 [偵錯]**** 功能表上的 [不進入函式]****。<br /><br /> 在 [**調試**] 工具列上，按一下 [**跳過**] 按鈕。<br /><br /> 按下 F10。|  
|跳離模組|在 [**調試**] 功能表上，按一下 [**跳出**]。<br /><br /> 在 [**調試**] 工具列上，按一下 [**跳出**] 按鈕。<br /><br /> 按下 SHIFT+F11。|  
|執行至目前的資料指標位置|在 [查詢編輯器] 視窗中按一下滑鼠右鍵，然後按一下 [執行至資料指標處]  。<br /><br /> 按下 CTRL+F10。|  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 偵錯工具資訊](transact-sql-debugger-information.md)  
  
  
