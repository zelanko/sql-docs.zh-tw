---
title: 使用解譯的 Transact-SQL 存取記憶體最佳化資料表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c81ac6c0c8dcf7e24c80b426654164c668fcf3a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124018"
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>使用解譯的 Transact-SQL 存取記憶體最佳化的資料表
  您可以使用任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢或 DML 作業 (SELECT、INSERT、UPDATE 或 DELETE)、特定批次以及 SQL 模組 (例如預存程序、資料表值函數、觸發程序和檢視表) 來存取記憶體最佳化的資料表，僅有一些例外狀況。  
  
 解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指的是非原生編譯預存程序的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次或預存程序。 記憶體最佳化資料表的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 解譯存取指的是 Interop 存取。  
  
 記憶體最佳化的資料表也可以透過原生編譯的預存程序存取。 建議針對效能嚴重不足的 OLTP 作業使用以原生方式編譯的預存程序。  
  
 建議在這些案例中使用解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取：  
  
-   隨選查詢和管理工作。  
  
-   報告查詢，通常會使用以原生方式編譯的預存程序中未提供的建構 (例如視窗函數)。  
  
-   為了將應用程式效能嚴重不足部分移轉至記憶體最佳化資料表，應用程式碼變更需求最低或完全不需要。 您可能會從移轉的資料表看到效能提升。 如果您之後將預存程序移轉到以原生方式編譯的預存程序，您可以查看進一步的效能改善情形。  
  
-   當以原生方式編譯的預存程序無法使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式時。  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建構在記憶體最佳化資料表中存取資料的解譯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序中不受支援。  
  
|區域|不支援|  
|----------|-----------------|  
|存取資料表|TRUNCATE TABLE<br /><br /> MERGE (做為目標之記憶體最佳化的資料表)。<br /><br /> 動態和索引鍵集資料指標 (這些會自動降級為靜態)。<br /><br /> 使用內容連接從 CLR 模組存取。<br /><br /> 從索引檢視表參考記憶體最佳化資料表。|  
|跨資料庫|跨資料庫查詢<br /><br /> 跨資料庫交易<br /><br /> 連結的伺服器|  
  
## <a name="table-hints"></a>資料表提示  
 如需有關資料表提示的詳細資訊，請參閱。 [資料表提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)。 新增支援 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 的快 SNAPSHOT 隔離。  
  
 使用解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)]存取記憶體最佳化的資料表時，不支援下列資料表提示。  
  
|||||  
|-|-|-|-|  
|HOLDLOCK|IGNORE_CONSTRAINTS|IGNORE_TRIGGERS|NOWAIT|  
|PAGLOCK|READCOMMITTED|READCOMMITTEDLOCK|READPAST|  
|READUNCOMMITTED|ROWLOCK|SPATIAL_WINDOW_MAX_CELLS = *integer*|TABLOCK|  
|TABLOCKXX|UPDLOCK|XLOCK||  
  
 當您使用解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 從明確或隱含交易存取記憶體最佳化的資料表時，您必須包括隔離等級的資料表提示，例如 SNAPSHOT、REPEATABLEREAD 或 SERIALIZABLE，或者，您可以使用 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT。 如需詳細資訊，請參閱[與記憶體最佳化資料表的交易隔離等級的指導方針](memory-optimized-tables.md)並[ALTER DATABASE SET 選項&#40;-&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
> [!NOTE]  
>  在自動認可模式下執行之查詢所存取的記憶體最佳化的資料表不需要隔離等級資料表提示。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體中 OLTP 的 Transact-SQL 支援](transact-sql-support-for-in-memory-oltp.md)   
 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  
