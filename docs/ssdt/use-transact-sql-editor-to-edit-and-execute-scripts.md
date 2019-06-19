---
title: 使用 Transact-SQL 編輯器，編輯及執行指令碼 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLEDITOR
ms.assetid: fa78e2cf-3c64-49f5-93cc-a3d50b1e7d05
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e348fba8c391b438c0429c8a32e167fd810b53d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65102066"
---
# <a name="use-transact-sql-editor-to-edit-and-execute-scripts"></a>使用 Transact-SQL 編輯器，編輯及執行指令碼
Transact\-SQL 編輯器為您在使用指令碼時提供豐富的編輯和偵錯體驗。 使用 [檢視程式碼] 快顯功能表開啟連線的資料庫或專案中的資料庫實體時，會叫用這個編輯器。 從 [SQL Server 物件總管] 使用 [新增查詢] 快顯功能表，或將新的指令碼物件加入至資料庫專案時，也會自動開啟這個編輯器。  
  
如果要對尚未連線的資料庫執行查詢，您也可以使用 [SQL] -> [Transact\-SQL 編輯器] 功能表選項中的 [新增查詢連接] 對話方塊，連線到資料庫並啟動 Transact\-SQL 編輯器。  
  
Transact\-SQL 編輯器包含撰寫及編輯 Transact\-SQL 指令碼的主要 [T-SQL] 窗格。 這個編輯器支援 IntelliSense 與語法色彩編碼，可以提高複雜陳述式的可讀性。 它還支援尋找和取代、大量註解、自訂字型和色彩，以及顯示行號。 您也可以變更編輯器中的指令碼執行依據的資料庫。 如需詳細資訊，請參閱[如何：複製現有的資料庫](../ssdt/how-to-clone-an-existing-database.md)。 [結果] 窗格會將查詢結果顯示在方格或文字中。 您也可以將查詢結果重新導向至檔案。 [訊息] 窗格會顯示指令碼執行時傳回的錯誤、警告和參考用訊息。 當用戶端統計資料已啟用時，[統計資料] 窗格會分類顯示查詢執行的資訊。 [執行計畫] 窗格會顯示 SQL Server 所選的資料擷取方法，並顯示特定陳述式與查詢的執行成本。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|---------|---------------|  
|[操作說明：概述並將程式碼片段新增至 Transact-SQL 指令碼](../ssdt/how-to-outline-and-add-snippets-to-transact-sql-script.md)|使用程式碼片段選擇器，將現成的 Transact\-SQL 程式碼插入查詢。|  
|[操作說明：在指令碼之間巡覽](../ssdt/how-to-navigate-between-scripts.md)|使用 [移至定義] 和 [尋找所有參考]，在指令碼之間巡覽。|  
|[操作說明：使用重新命名和重構以變更資料庫物件](../ssdt/how-to-use-rename-and-refactoring-to-make-changes-to-your-database-objects.md)|跨所有指令碼重新命名物件，並預覽任何變更。|  
|[操作說明：執行部分查詢](../ssdt/how-to-execute-a-partial-query.md)|以反白顯示指令碼的特定區段，並且將它執行成單一查詢。|  
|[操作說明：針對預存程序進行偵錯](../ssdt/how-to-debug-stored-procedures.md)|藉由逐步執行來建立 Transact\-SQL 及對它進行偵錯。|  
|[分析指令碼效能](../ssdt/analyze-script-performance.md)|使用執行計畫、用戶端統計資料和程式碼分析，判斷是否能提升查詢、預存程序或指令碼的效能。|  
  
## <a name="see-also"></a>另請參閱  
[操作說明：使用查詢建立新的資料庫物件](../ssdt/how-to-create-new-database-objects-using-queries.md)  
  
