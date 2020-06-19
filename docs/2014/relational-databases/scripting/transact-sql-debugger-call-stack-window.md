---
title: 呼叫堆疊視窗
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Call Stack Window [Transact-SQL]
ms.assetid: ddb0b19c-87cd-4883-bcb8-ec09ffb30369
author: rothja
ms.author: jroth
ms.openlocfilehash: 720a42b2b3ddf46318ac5412181d70a79b142026
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063360"
---
# <a name="call-stack-window"></a>呼叫堆疊視窗
  [呼叫堆疊]  視窗會顯示呼叫堆疊上的模組以及傳遞給模組之任何參數的資料類型和值。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 模組包括預存程序、函數及觸發程序 若要顯示呼叫堆疊，您必須在偵錯模式中。  
  
## <a name="task-list"></a>工作清單  
 **存取呼叫堆疊視窗**  
  
-   在 [偵錯]  功能表上，按一下 [視窗]  ，然後按一下 [呼叫堆疊]  。  
  
 **變更目前的呼叫堆疊框架**  
  
 您可以使用以下程序的其中一種，讓堆疊框架變成目前的框架：  
  
-   以滑鼠右鍵按一下堆疊框架，然後按一下 [切換至框架]  。  
  
-   按兩下此堆疊框架。  
  
 **檢視目前框架以外之框架的來源**  
  
-   以滑鼠右鍵按一下堆疊框架，然後按一下 [移至原始程式碼]  。  
  
## <a name="stack-frames"></a>堆疊框架  
 [呼叫堆疊]  視窗中的每一個資料列都稱為堆疊框架，而且代表從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案到模組的呼叫或是從某個模組到另一個模組的呼叫。 顯示畫面底部的堆疊框架表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [查詢編輯器] 視窗中對此堆疊進行第一個呼叫的那一行。 頂端列表示偵錯工具暫停執行的那一行，而且是由視窗左邊界的黃色箭頭所識別。 每一個中間列都表示呼叫下一個更高堆疊框架之原始程式碼的模組和行號。  
  
 [區域變數]  、[監看式]  和 [快速監看式]  視窗中的所有運算式都會根據目前的堆疊框架來評估。 [查詢編輯器] 視窗會顯示目前框架的程式碼。 根據預設，目前的堆疊框架就是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具暫停執行所在的框架。 當您將目前的堆疊框架變更為另一個框架時，將會在新框架的內容中重新評估 [區域變數]  、[監看式]  和 [快速監看式]  視窗中的運算式，而且新框架的原始程式碼會顯示在 [查詢編輯器] 視窗中。  
  
## <a name="columns"></a>資料行  
 **名稱**  
 顯示有關呼叫堆疊上之模組的資訊。  
  
 如果是呼叫堆疊內的底部列，[名稱]  會列出 [查詢編輯器] 來源視窗及第一次呼叫此堆疊的行號。 如果是其他資料列，[名稱]  的格式為 **Module(Instance.Database)(ParmList) LineNumber**。  
  
 **模組**  
 這是預存程序、函數或呼叫下一個堆疊之預存程序的名稱。  
  
 **Instance.Database**  
 這是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體以及保留模組的資料庫。  
  
 **ParmList**  
 表示在模組的呼叫期間所傳入之每一個參數的資料類型、名稱和值。  
  
 **LineNumber**  
 如果是頂端列以外的所有列， **LineNumber** 表示模組中呼叫此框架的那一行。 如果是頂端列， **LineNumber** 表示偵錯工具目前焦點所在的那一行。  
  
 **語言**  
 顯示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的 [Transact-SQL]。  
  
## <a name="see-also"></a>另請參閱  
 [Transact-sql 偵錯工具](transact-sql-debugger.md)   
 [Transact-sql 偵錯工具資訊](transact-sql-debugger-information.md)   
 [逐步執行 Transact-SQL 程式碼](step-through-transact-sql-code.md)  
