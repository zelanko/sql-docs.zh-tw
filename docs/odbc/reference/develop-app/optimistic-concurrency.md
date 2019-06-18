---
title: 開放式並行存取 |Microsoft Docs
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
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa80ff3359e3bbbed9e28044cce7514006c40f10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446210"
---
# <a name="optimistic-concurrency"></a>開放式並行存取
*開放式並行存取*是它的名稱衍生自樂觀的假設，很少會發生交易之間的衝突; 已在更新或刪除的資料，它唯讀的時間之間的資料列的另一個交易時所發生所謂的衝突目前的交易和時間所更新或刪除。 它是相對於*封閉式並行存取，* 鎖定，或在其應用程式開發人員認為這類衝突是老生常談。  
  
 開放式並行存取，資料列處於已解除鎖定，直到要在更新或刪除它。 此時，資料列會重新讀取，並檢查，以查看是否它之後已經變更上次讀取。 如果資料列已變更，更新或刪除就會失敗，而且必須重試。  
  
 若要判斷是否已經變更一個資料列，其新的版本會檢查對該資料列的快取版本。 這項檢查可以根據資料列版本，例如 SQL Server，或資料列中的每個資料行的值時間戳記資料行。 有許多 Dbms 不支援資料列版本。  
  
 資料來源或應用程式可以實作開放式並行存取。 在任一情況下，應用程式應該使用例如 Read Committed; 較低的交易隔離等級使用較高的層級，可以避免使用開放式並行存取獲得提升並行數。  
  
 如果資料來源來實作開放式並行存取，應用程式會將 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES 設定 SQL_ATTR_CONCURRENCY 陳述式屬性。 若要更新或刪除資料列，它會執行定位的 update 或 delete 陳述式或呼叫**SQLSetPos**的驅動程式或資料來源就如同使用封閉式並行存取; 如果傳回 SQLSTATE 01001 （資料指標作業衝突）更新或刪除 因衝突而失敗。  
  
 如果應用程式本身會實作開放式並行存取，它會 SQL_CONCUR_READ_ONLY 讀取資料列，以設定 SQL_ATTR_CONCURRENCY 陳述式屬性。 如果它將會比較資料列版本，而不知道的資料列版本資料行，則會呼叫**SQLSpecialColumns** SQL_ROWVER 選項，以判斷此資料行名稱。  
  
 在應用程式更新或刪除資料列增加 SQL_CONCUR_LOCK （若要取得資料列的 「 寫入 」 權限），並執行並行**更新**或**刪除**陳述式搭配**位置**應用程式可以讀取它時發生子句所指定的版本，或資料列的值。 如果資料列已變更之後，將會失敗，陳述式。 如果**其中**子句不會唯一識別資料列、 陳述式也可能會更新或刪除其他資料列; 資料列版本一定會唯一識別資料列，但資料列值唯一識別資料列，只有當它們包含的主索引鍵。
