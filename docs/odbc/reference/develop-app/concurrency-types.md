---
title: 並行類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12891d7ee674167157bcb02300d2e4181ef51734
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63012119"
---
# <a name="concurrency-types"></a>並行類型
若要解決資料指標中的並行性降低的問題，ODBC 會公開資料指標並行的四種不同的類型：  
  
-   **唯讀**資料指標可以讀取資料，但無法更新或刪除資料。 這是預設並行類型。 雖然 DBMS 可能會鎖定來強制執行 Repeatable Read 和 Serializable 隔離等級的資料列，它可以使用讀取的鎖定，而不是寫入鎖定。 這會導致較高的並行存取，因為其他交易至少可以讀取資料。  
  
-   **鎖定**資料指標使用鎖定以確定它可以更新或刪除資料列在結果集中所需的最低層級。 這通常會導致非常低的並行存取等級，尤其是在 Repeatable Read 和 Serializable 交易隔離等級。  
  
-   **使用資料列版本的開放式並行存取和使用值的開放式並行存取**資料指標使用開放式並行存取：它會更新，或它們沒有任何變更自上次讀取後，才會刪除資料列。 若要偵測的變更，它會比較資料列版本或值。 則無法保證資料指標可以更新或刪除資料列，但並行是遠高於時使用鎖定。 如需詳細資訊，請參閱下一節[開放式並行存取](../../../odbc/reference/develop-app/optimistic-concurrency.md)。  
  
 應用程式指定它想要的游標 SQL_ATTR_CONCURRENCY 陳述式屬性搭配使用何種類型的並行存取。 若要判斷支援哪些類型，它會呼叫**SQLGetInfo** SQL_SCROLL_CONCURRENCY 選項。
