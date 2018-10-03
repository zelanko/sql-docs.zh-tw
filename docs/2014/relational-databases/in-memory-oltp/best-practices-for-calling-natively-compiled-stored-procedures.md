---
title: 呼叫原生編譯預存程序的最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1dbc3dd467aab0cf60cdb255165767fc12a0f518
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048528"
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
  
 透過 XEvent `hekaton_slow_parameter_passing` 與 `reason=named_parameters`，可偵測到 (無效率的) 具名參數與原生編譯預存程序的使用方式。  
  
 同樣地，您可以在此偵測使用不相符的類型，透過相同的 XEvent `hekaton_slow_parameter_passing`，使用`reason=parameter_conversion`。  
  
 因為在使用記憶體最佳化資料表時必須實作重試邏輯 (在許多案例中)，而且因為您必須避開某些功能限制，所以您可能會想要建立包裝函式解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序。 如需範例，請參閱[Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](memory-optimized-tables.md)。  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](natively-compiled-stored-procedures.md)  
  
  
