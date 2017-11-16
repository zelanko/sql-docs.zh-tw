---
title: "呼叫原生編譯預存程序的最佳做法 | Microsoft Docs"
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 99824ee6f0ca42b200cda37589c30df9b9434cba
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>呼叫原生編譯預存程序的最佳作法
  原生編譯預存程序：  
  
-   通常用於應用程式的關鍵性效能組件中。  
  
-   經常執行。  
  
-   預期非常快速。  
  
 使用原生編譯預存程序的效能優勢，會隨程序所處理的資料列數目和邏輯數量增多而提升。 例如，如果原生編譯預存程序使用下列一個或多個項目，則會展現更佳的效能：  
  
-   彙總。  
  
-   巢狀迴圈聯結。  
  
-   多重陳述式選取、插入、更新和刪除作業。  
  
-   複雜運算式。  
  
-   程序邏輯，例如條件陳述式和迴圈。  
  
 如果您只需要處理一個資料列，使用原生編譯預存程序可能不會提供效能優勢。  
  
 若要避免伺服器必須對應參數名稱和轉換類型：  
  
-   讓傳遞至程序的參數類型與程序定義中的類型相符。  
  
-   當呼叫原生編譯預存程序時，請使用序數 (無名) 參數。 若要以最有效率方式執行，請勿使用具名參數。  
  
 原生編譯預存程序參數中的無效率情況，可以透過 XEvent **natively_compiled_proc_slow_parameter_passing** 加以偵測：
 - 類型不符︰**reason=parameter_conversion**
 - 具名參數：**reason=named_parameters**
 - 預設值：**reason=default** 
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
