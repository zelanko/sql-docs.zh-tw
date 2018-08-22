---
title: 原生編譯的預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
caps.latest.revision: 54
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 79dbaba00d9eb8ff0b344fb713ee6599344ec317
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394011"
---
# <a name="natively-compiled-stored-procedures"></a>原生編譯的預存程序
  原生編譯預存程序是編譯成可存取記憶體最佳化資料表之機器碼的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序。 原生編譯預存程序提供以有效率的方式執行預存程序中的查詢與商務邏輯。 如需有關原生編譯程序的詳細資料，請參閱＜ [Native Compilation of Tables and Stored Procedures](native-compilation-of-tables-and-stored-procedures.md)＞。 如需有關將以磁碟為基礎之預存程序移轉至原生編譯預存程序的詳細資訊，請參閱＜ [Migration Issues for Natively Compiled Stored Procedures](migration-issues-for-natively-compiled-stored-procedures.md)＞。  
  
> [!NOTE]  
>  解譯 (以磁碟為基礎) 的預存程序與原生編譯的預存程序之間的差異在於，解譯的預存程序是在第一次執行時編譯，而原生編譯的預存程序是在建立時編譯。 原生編譯的預存程序於建立時將能偵測出許多錯誤狀況 (算術溢位、類型轉換和一些除以零的狀況)，而這會造成原生編譯的預存程序建立失敗。 若是解譯的預存程序，則這些錯誤狀況通常不會導致預存程序建立失敗，不過所有的執行都將失敗。  
  
 本節主題：  
  
-   [建立原生編譯的預存程序](creating-natively-compiled-stored-procedures.md)  
  
-   [不可部分完成的區塊](atomic-blocks-in-native-procedures.md)  
  
-   [原生編譯的預存程序中支援的建構](supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [在原生編譯預存程序中使用 Try..Catch](../../database-engine/using-try-catch-in-natively-compiled-stored-procedures.md)  
  
-   [原生編譯的預存程序上支援的建構](supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [原生編譯的預存程序和執行 Set 選項](natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [呼叫原生編譯預存程序的最佳作法](best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [監視原生編譯預存程序的效能](monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [從資料存取應用程式呼叫原生編譯預存程序](calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表](memory-optimized-tables.md)  
  
  
