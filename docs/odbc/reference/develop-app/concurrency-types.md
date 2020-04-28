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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 642301d09c5aa189276db534e58aca0c5e00e3ce
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299098"
---
# <a name="concurrency-types"></a>並行類型
為了解決資料指標中減少平行存取的問題，ODBC 會公開四種不同類型的資料指標並行：  
  
-   **唯讀**游標可以讀取資料，但無法更新或刪除資料。 這是預設的並行類型。 雖然 DBMS 可能會鎖定資料列，以強制執行可重複讀取和可序列化的隔離等級，但是它可以使用讀取鎖定，而不是寫入鎖定。 這會導致平行存取較高，因為其他交易至少可以讀取資料。  
  
-   **鎖定**資料指標會使用所需的最低層級鎖定，確保它可以更新或刪除結果集中的資料列。 這通常會導致非常低的並行層級，特別是在可重複讀取和可序列化的交易隔離等級。  
  
-   **使用資料列版本的開放式平行存取和使用值的開放式並行**存取資料指標使用開放式平行存取：它會更新或刪除資料列，但只有在上次讀取之後，才會進行變更。 若要偵測變更，它會比較資料列版本或值。 不保證資料指標可以更新或刪除資料列，但是並行處理的速度遠高於使用鎖定的時間。 如需詳細資訊，請參閱下一節[開放式並行](../../../odbc/reference/develop-app/optimistic-concurrency.md)存取。  
  
 應用程式會指定要讓資料指標與 SQL_ATTR_CONCURRENCY 語句屬性搭配使用的並行類型。 為了判斷支援哪些類型，它會使用 SQL_SCROLL_CONCURRENCY 選項來呼叫**SQLGetInfo** 。
