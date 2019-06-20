---
title: 查詢選項執行 （進階頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f08758af9c75e36dbf8c8d4d62ae17352972b79d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089089"
---
# <a name="query-options-execution-advanced-page"></a>查詢選項執行 (進階頁面)
  使用 **SET** 陳述式時，有許多選項可用。 使用此頁面來指定 **set** 選項，以執行 Microsoft SQL Server 查詢。 如需上述各選項的詳細資訊，請參閱《SQL Server 線上叢書》。  
  
 **SET NOCOUNT**  
 不會以結果集的訊息傳回資料列數的計數。 依預設，會清除此選項。  
  
 **SET NOEXEC**  
 不會執行查詢。 依預設，會清除此選項。  
  
 **SET PARSEONLY**  
 檢查每個查詢的語法，但不會執行查詢。 依預設，會清除此選項。  
  
 **SET CONCAT_NULL_YIELDS_NULL**  
 如果選取此核取方塊，串連現有值與 `NULL` 的查詢，一律會傳回 `NULL` 的結果。 如果清除此核取方塊，現有的值與 `NULL` 串連，則會傳回現有的值。 預設會選取此選項。  
  
 **SET ARITHABORT**  
 如果選取此核取方塊，`INSERT`、`DELETE` 或 `UPDATE` 陳述式在運算式評估期間發現算術錯誤 (溢位、除以零或網域錯誤) 時，就會結束查詢或批次。 如果清除此核取方塊，在可能的情況下就會為該值提供 `NULL`，而查詢會繼續進行，並在結果中包含訊息。 請參閱線上叢書，以取得此行為的詳細描述。 預設會選取此選項。  
  
 **SET SHOWPLAN_TEXT**  
 如果選取此核取方塊，查詢計畫就會以文字格式傳回每個查詢。 依預設，會清除此選項。  
  
 **SET STATISTICS TIME**  
 如果選取此核取方塊，則每個查詢就會一併傳回時間統計資料。 依預設，會清除此選項。  
  
 **SET STATISTICS IO**  
 如果選取此核取方塊，則每個查詢就會傳回關於輸入/輸出 (I/O) 的統計資料。 依預設，會清除此選項。  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 依預設，會設定 READ COMMITTED 交易隔離等級。 如需詳細資訊，請參閱 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。 無法使用 SNAPSHOT 交易隔離等級。 若要使用 SNAPSHOT 隔離，請加入下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式：  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **集合的死結優先權**  
 預設值為 **Normal**，可在死結發生時讓每個查詢都有相同的優先權。 如果您要此查詢在發生任何死結衝突時失敗，並選取為要結束的查詢，請從下拉式清單中選取「低」優先權。  
  
 **設定鎖定逾時**  
 預設值 -1 指出完成交易之前會保持鎖定。 值為 0 表示根本不等候，並在發生鎖定時立刻傳回訊息。 提供大於 0 毫秒的值，即可指定當交易的鎖定時間超過指定值，就結束交易。  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 使用 [查詢管理員成本限制] 選項，指定查詢可執行的時間週期上限。 查詢成本代表在特定的硬體組態上，預估完成查詢所需的時間 (以秒為單位)。 預設值為 0 表示查詢執行沒有時間長度的限制  
  
 **隱藏提供者訊息標頭**  
 選取此核取方塊時，不會顯示來自提供者 (例如 OLE DB 提供者) 的狀態訊息。 依預設，這個核取方塊為已選取。 當疑難排解查詢於提供者層級失敗時，清除此核取方塊即可查看提供者訊息。  
  
 **查詢執行後中斷連接**  
 如果選取此核取方塊，查詢完成後會結束 SQL Server 的連接。 依預設，會清除此選項。  
  
 **重設為預設值**  
 將此頁面上的所有值重設為原始預設值。  
  
  
