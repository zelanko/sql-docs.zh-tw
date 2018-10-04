---
title: 選項 (查詢執行： SQL Server︰ 進階頁面) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAdvanced
ms.assetid: 3ec788c7-22c3-4216-9ad0-81a168d17074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 2b2268b945b6b4eb2f82ed3d517be01bb2ec750c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067400"
---
# <a name="options-query-executionsql-serveradvanced-page"></a>選項 (查詢執行：SQL Server：進階頁面)
  使用 SET 命令有許多選項可用。 使用此頁面來指定 **設定** 選項，以在 SQL Server 查詢編輯器中執行 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢。 它們對於其他程式碼編輯器沒有影響。 這些選項的變更僅適用於新的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢。 若要變更目前查詢的選項，請按一下 **[查詢]** 功能表上的 **[查詢選項]** ，或按一下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢視窗的快速鍵功能表。 在 **[執行]** 下，按一下 **[進階]**。 如需上述各項目的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》。  
  
## <a name="options"></a>選項。  
 **SET NOCOUNT**  
 不會以結果集的訊息傳回資料列數的計數。 依預設，不會勾選此核取方塊。  
  
 **SET NOEXEC**  
 不會執行查詢。 依預設，不會勾選此核取方塊。  
  
 **SET PARSEONLY**  
 檢查每個查詢的語法，但不會執行查詢。 依預設，不會勾選此核取方塊。  
  
 **SET CONCAT_NULL_YIELDS_NULL**  
 如果選取此核取方塊，串連現有值與 NULL 的查詢，一律會傳回 NULL 的結果。 如果清除此核取方塊，現有的值與 NULL 串連，則會傳回現有的值。 依預設，這個核取方塊為已選取。  
  
 **SET ARITHABORT**  
 如果選取此核取方塊，INSERT、DELETE 或 UPDATE 陳述式在運算式評估期間發現算術錯誤 (溢位、除以零或網域錯誤) 時，就會結束查詢或批次。 如果清除此核取方塊，在可能的情況下就會為該值提供 NULL，而查詢會繼續進行，並在結果中包含訊息。 如需詳細資訊，請參閱 [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql)。 依預設，這個核取方塊為已選取。  
  
 **SET SHOWPLAN_TEXT**  
 如果選取此核取方塊，查詢計畫就會以文字格式傳回每個查詢。 依預設，不會勾選此核取方塊。  
  
 **SET STATISTICS TIME**  
 如果選取此核取方塊，則每個查詢就會一併傳回時間統計資料。 依預設，不會勾選此核取方塊。  
  
 **SET STATISTICS IO**  
 如果選取此核取方塊，則每個查詢就會傳回關於輸入與輸出的統計資料。 依預設，不會勾選此核取方塊。  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 依預設，會設定 READ COMMITTED 交易隔離等級。 如需詳細資訊，請參閱 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。 無法使用 SNAPSHOT 交易隔離等級。 若要使用 SNAPSHOT 隔離，請加入下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式：  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **集合的死結優先權**  
 預設值為「標準」，可在死結發生時讓每個查詢都有相同的優先權。 如果您要此查詢在發生任何死結衝突時失敗，並選取為要結束的查詢，請選取「低」優先權。  
  
 **設定鎖定逾時**  
 預設值 -1 指出完成交易之前會保持鎖定。 值為 0 表示根本不等候，並在發生鎖定時立刻傳回訊息。 提供大於 0 毫秒的值，即可指定當交易的鎖定時間超過指定值，就結束交易。  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 使用 **QUERY_GOVERNOR_COST_LIMIT** 選項，即可指定查詢執行的時間上限。 查詢成本代表在特定的硬體組態上，預估完成查詢所需的時間 (以秒為單位)。 預設值為 0 表示查詢執行沒有時間長度的限制。  
  
 **隱藏提供者訊息標頭**  
 選取此核取方塊時，不會顯示來自提供者 (例如 SQLClient 提供者) 的狀態訊息。 依預設，這個核取方塊為已選取。 當疑難排解查詢於提供者層級失敗時，清除此核取方塊即可查看提供者訊息。  
  
 **查詢執行後中斷連接**  
 如果選取此核取方塊，查詢完成後會結束 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的連接。 依預設，不會勾選此核取方塊。  
  
 **重設為預設值**  
 將此頁面上的所有值重設為原始預設值。  
  
  
