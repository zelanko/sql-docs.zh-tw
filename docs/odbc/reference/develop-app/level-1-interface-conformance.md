---
title: 等級 1 介面一致性 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d31d5fe8aea1df4e7937104580efb820ba6f031
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306179"
---
# <a name="level-1-interface-conformance"></a>層級 1 介面一致性
級別 1 介面一致性級別包括核心介面一致性級別功能以及通常可在 OLTP 關係 DBMS 中提供的其他功能(如事務)。 除了 Core 介面一致性等級中的功能外,1 層介面一致性驅動程式還允許應用程式執行以下操作:  
  
|||  
|-|-|  
|101|指定資料庫表和檢視的架構(使用由兩部分組成的命名)。 (有關詳細資訊,請參閱[級別 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的由三部分組成的命名功能 201 。|  
|102|呼叫 ODBC 函數的真實非同步執行,如果適用的 ODBC 函數是同步的或給定連接上的所有異步函數。|  
|103|使用可滾動遊標,從而通過使用SQL_FETCH_NEXT以外的*Fetch 定向*參數調用**SQLFetchScroll,** 從而在非正向方法中實現對結果集的訪問。 (SQL_FETCH_BOOKMARK*提取方向*位於[2 層介面符合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能 204 中 。|  
|104|通過調用**SQL 主要密鑰**獲取表的主鍵。|  
|105|通過 ODBC 轉義序列對過程呼叫使用儲存過程,並透過調用**SQLProcess 列**和**SQL 程式**查詢有關儲存過程的數據字典。 (在數據源上創建和存儲過程的過程不在本文檔的範圍之內。|  
|106|通過呼叫**SQLBrowseConnect,** 透過互動式瀏覽可用伺服器連接到資料來源。|  
|107|使用 ODBC 函數而不是 SQL 語句來執行某些資料庫操作:具有SQL_POSITION的**SQLSetPos**和SQL_REFRESH。|  
|108|通過調用**SQLMoreResult**獲取對批次處理和儲存過程生成的多個結果集內容的訪問。|  
|109|分隔跨越多個 ODBC 函數的事務,具有真正的原子性和在**SQLEndTran**中指定SQL_ROLLBACK的能力。|
