---
title: "開放式並行存取 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 422f16155f79b61a7cc46516d8a4e7deb2fe19f9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="optimistic-concurrency"></a>開放式並行存取
*開放式並行存取*是它的名稱衍生自在開放式假設，很少會發生交易之間發生衝突，衝突稱為時發生另一個交易中更新或刪除資料列之間的時間會在讀取的資料它是由目前的交易和時間來更新或刪除。 它是相反的*封閉式並行存取，*鎖定，或在其應用程式開發人員認為這類衝突很常見。  
  
 在開放式並行存取，資料列處於已解除鎖定，直到卻要更新或刪除它。 此時，會重新讀取及檢查，以查看是否它已被變更自從上次讀取之後的資料列。 如果資料列已變更，更新或刪除失敗，且必須重試。  
  
 若要判斷是否已經變更一個資料列，其新的版本會核對快取的資料列版本。 這項檢查可以根據資料列版本，例如 SQL Server 或資料列中的每個資料行的值中的時間戳記資料行。 有許多 Dbms 不支援資料列版本。  
  
 資料來源或應用程式可以實作開放式並行存取。 在任一情況下，應用程式應該使用不足的交易隔離等級 Read Committed; 例如使用較高的層級否定使用開放式並行存取模式而獲得的增加的並行。  
  
 如果資料來源實作開放式並行存取時，應用程式會設定 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY 陳述式屬性。 若要更新或刪除資料列，它會執行定位的更新或刪除陳述式或呼叫**SQLSetPos**的驅動程式或資料來源便能夠與封閉式並行存取; 如果傳回 SQLSTATE 01001 （資料指標作業衝突）更新或刪除因為衝突而失敗。  
  
 如果應用程式本身會實作開放式並行存取，將陳述式屬性 SQL_ATTR_CONCURRENCY 設 SQL_CONCUR_READ_ONLY 讀取資料列。 它會比較資料列版本，而不知道資料列版本資料行，它會呼叫**SQLSpecialColumns** SQL_ROWVER 選項，以判斷此資料行的名稱。  
  
 應用程式更新或刪除資料列，藉由增加並行模式設為 SQL_CONCUR_LOCK （若要取得資料列的寫入權限） 並執行**更新**或**刪除**陳述式搭配**位置**子句所指定的版本，或值的資料列時發生應用程式可以讀取它。 如果資料列已變更從那時起，陳述式會失敗。 如果**其中**子句並未識別唯一資料列、 陳述式也可能會更新或刪除其他資料列; 資料列版本一定唯一識別資料列，但資料列值唯一識別資料列，只有當它們包含的主索引鍵。
