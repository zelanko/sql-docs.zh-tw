---
title: 記憶體最佳化資料表 | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14dddf81-b502-49dc-a6b6-d18b1ae32d2b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9123bf89f75fce68a6edd8ba1becd141821fe326
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227858"
---
# <a name="memory-optimized-tables"></a>記憶體最佳化的資料表
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體中 OLTP 可透過有效率的記憶體最佳化資料存取、商務邏輯的原生編譯以及不需鎖定與閂鎖的演算法，協助提升 OLTP 應用程式的效能。 記憶體中 OLTP 功能包括記憶體最佳化資料表和資料表類型，以及 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序的原生編譯，能夠有效率地存取這些資料表。  
  
 如需有關記憶體最佳化的資料表的詳細資訊，請參閱：  
  
-   [記憶體最佳化的資料表簡介](memory-optimized-tables.md)  
  
     詳述何謂記憶體最佳化資料表，並提供資料持久性及存取記憶體最佳化資料表中資料的相關資訊，以及效能與延展性的資訊。  
  
-   [資料表和預存程序的原生編譯](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
     詳述記憶體最佳化資料表及原生編譯預存程序編譯至 DLL 中的方法，並提供相關安全性考量。  
  
-   [改變記憶體最佳化資料表](altering-memory-optimized-tables.md)  
  
     升級記憶體最佳化資料表的方針 (包含變更資料行、索引及 bucket_count)。  
  
-   [了解經記憶體最佳化的資料表上的交易](../../database-engine/understanding-transactions-on-memory-optimized-tables.md)  
  
     本節提供數個有關對記憶體最佳化資料表執行交易的主題，包含交易隔離等級，以及跨容器的交易。  
  
-   [分割記憶體最佳化資料表的應用程式模式](application-pattern-for-partitioning-memory-optimized-tables.md)  
  
     詳細的程式碼範例，示範使用記憶體最佳化資料表時，如何模擬資料分割資料表。  
  
-   [記憶體最佳化資料表的統計資料](statistics-for-memory-optimized-tables.md)  
  
     詳述如何為記憶體最佳化資料表編譯統計資料，以及如何為記憶體最佳化資料表維護及手動更新統計資料。  
  
-   [定序和字碼頁](../../database-engine/collations-and-code-pages.md)  
  
     詳述受支援定序的限制，以及記憶體最佳化資料表的字碼頁。  
  
-   [記憶體最佳化資料表中的資料表和資料列大小](table-and-row-size-in-memory-optimized-tables.md)  
  
     詳述記憶體最佳化資料列的 8060 位元組限制，並提供計算資料表與資料列大小的範例。  
  
-   [記憶體最佳化資料表的查詢處理指南](a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
     針對記憶體最佳化資料表與原生編譯的預存程序，提供查詢處理的概觀。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
