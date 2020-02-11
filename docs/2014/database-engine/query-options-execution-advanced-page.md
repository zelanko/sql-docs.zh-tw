---
title: 查詢選項執行（Advanced Page） |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: ''
ms.date: 09/03/2019
ms.openlocfilehash: 39a43adeb82b154a076fc7bfc24cc56b54cc8640
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "71199322"
---
# <a name="query-options-execution-advanced-page"></a>查詢選項執行 (進階頁面)

  使用 **SET** 陳述式時，有許多選項可用。 使用此頁面來指定**SET**選項，以執行 Microsoft SQL Server 查詢。 如需上述各選項的詳細資訊，請參閱《SQL Server 線上叢書》。
  
**設定 NOCOUNT**不會傳回資料列數目的計數，做為包含結果集的訊息。 依預設，會清除此選項。

**設定 NOEXEC**不會執行查詢。 依預設，會清除此選項。

**設定 PARSEONLY**檢查每個查詢的語法，但不執行查詢。 依預設，會清除此選項。  

**設定 CONCAT_Null_YIELDS_Null**選取此核取方塊時，串連現有值與的`NULL`查詢，一律會傳回`NULL`做為結果。 如果清除此核取方塊，現有的值與 `NULL` 串連，則會傳回現有的值。 預設會選取此選項。

**設定 ARITHABORT**當選取這個核取方塊時，當`INSERT`、 `DELETE`或`UPDATE`語句在運算式評估期間遇到算術錯誤（溢位、零除或網域錯誤）時，就會終止查詢或批次。 如果清除此核取方塊，在可能的情況下就會為該值提供 `NULL`，而查詢會繼續進行，並在結果中包含訊息。 請參閱線上叢書，以取得此行為的詳細描述。 預設會選取此選項。
  
**設定 SHOWPLAN_TEXT**選取這個核取方塊時，會以文字形式傳回查詢計劃與每個查詢。 依預設，會清除此選項。
  
**設定統計資料時間**選取此核取方塊時，每個查詢都會傳回時間統計資料。 依預設，會清除此選項。
  
**設定統計資料 IO**如果選取此核取方塊，每個查詢都會傳回關於輸入/輸出（i/o）的統計資料。 依預設，會清除此選項。
  
**設定交易隔離等級**預設會設定讀取認可的交易隔離等級。 如需詳細資訊，請參閱 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。 無法使用快照集交易隔離等級。 若要使用 SNAPSHOT 隔離，請加入下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式：
  
  ```sql
  SET TRANSACTION ISOLATION LEVEL SNAPSHOT;
  GO
  ```

**設定鎖死優先順序**預設值為 [**一般**]，可讓每個查詢在發生鎖死時擁有相同的優先順序。 如果您要此查詢在發生任何死結衝突時失敗，並選取為要結束的查詢，請從下拉式清單中選取「低」優先權。

**設定鎖定超時**預設值-1 表示會保留鎖定，直到交易完成為止。 值為 0 表示根本不等候，並在發生鎖定時立刻傳回訊息。 提供大於 0 毫秒的值，即可指定當交易的鎖定時間超過指定值，就結束交易。

**設定 QUERY_GOVERNOR_COST_LIMIT**使用 [**查詢管理員成本限制**] 選項，即可指定查詢可以執行的時間週期上限。 查詢成本代表在特定的硬體組態上，預估完成查詢所需的時間 (以秒為單位)。 預設值為 0 表示查詢執行沒有時間長度的限制

**隱藏提供者訊息標頭**如果選取此核取方塊，就不會顯示來自提供者（例如 OLE DB 提供者）的狀態訊息。 依預設，這個核取方塊為已選取。 當疑難排解查詢於提供者層級失敗時，清除此核取方塊即可查看提供者訊息。

**查詢執行後中斷**連線選取此核取方塊時，SQL Server 的連接會在查詢完成後終止。 依預設，會清除此選項。

**顯示完成時間**可讓您在查詢結果之後或 [訊息] 索引標籤中，列印查詢執行完成的時間。

**適用于 Always Encrypted 的 VBS 記憶體保護區證明通訊協定**可讓您為 always Encrypted 與安全記憶體保護區所使用的虛擬化安全性（VBS）記憶體保護區設定證明通訊協定。

目前支援的證明通訊協定為：

* 主機守護者服務-使用 Windows 主機守護者服務（HGS）的證明通訊協定。

如需詳細資訊，請參閱[使用 secure 記憶體保護區](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions)和[secure 記憶體保護區證明](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions#secure-enclave-attestation)Always Encrypted。

**重設為預設值**將此頁面上的所有值重設為原始的預設值。
