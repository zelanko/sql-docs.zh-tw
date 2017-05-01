---
title: "原生編譯的預存程序 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
caps.latest.revision: 54
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b718bafa35ae753eba0064db2af168054fd211ca
ms.lasthandoff: 04/11/2017

---
# <a name="natively-compiled-stored-procedures"></a>原生編譯的預存程序
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  原生編譯預存程序是編譯成可存取記憶體最佳化資料表之機器碼的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序。 原生編譯預存程序允許以有效率的方式執行預存程序中的查詢和商務邏輯。 如需有關原生編譯程序的詳細資料，請參閱＜ [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md)＞。 如需將以磁碟為基礎之預存程序移轉至原生編譯預存程序的詳細資訊，請參閱 [原生編譯預存程序的移轉問題](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)。  
  
> [!NOTE]  
>  解譯 (以磁碟為基礎) 的預存程序與原生編譯的預存程序之間的差異在於，解譯的預存程序是在第一次執行時編譯，而原生編譯的預存程序是在建立時編譯。 原生編譯的預存程序於建立時將能偵測出許多錯誤狀況，而這會造成原生編譯的預存程序建立失敗 (例如算術溢位、類型轉換和一些除以零的狀況)。 若是解譯的預存程序，這些錯誤狀況通常不會導致預存程序建立失敗，但所有的執行都會失敗。  
  
 本節主題：  
  
-   [建立原生編譯的預存程序](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)  
  
-   [不可部分完成的區塊](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)  
  
-   [原生編譯的 T-SQL 模組支援的功能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [原生編譯 T-SQL 模組支援的 DDL](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [原生編譯的預存程序和執行 Set 選項](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [呼叫原生編譯預存程序的最佳作法](../../relational-databases/in-memory-oltp/best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [監視原生編譯預存程序的效能](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [從資料存取應用程式呼叫原生編譯預存程序](../../relational-databases/in-memory-oltp/calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
