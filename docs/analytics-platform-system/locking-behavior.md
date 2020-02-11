---
title: 鎖定行為
description: 瞭解平行資料倉儲如何使用鎖定來確保交易的完整性，以及在多個使用者同時存取資料時，維護資料庫的一致性。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f3ecf5cf783b707b75c90dfa70d502e3c81d28c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401005"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>平行處理資料倉儲中的鎖定行為
瞭解平行資料倉儲如何使用鎖定來確保交易的完整性，以及在多個使用者同時存取資料時，維護資料庫的一致性。  
  
## <a name="Basics"></a>鎖定基本概念  
**方式**  
  
SQL Server PDW 支援四種鎖定模式：  
  
獨佔  
獨佔鎖定會禁止寫入或讀取鎖定的物件，直到保存獨佔鎖定的交易完成為止。 當獨佔鎖定生效時，不允許任何模式的其他鎖定。 例如，DROP TABLE 和 CREATE DATABASE 會使用獨佔鎖定。  
  
共用  
共用鎖定會禁止起始受影響物件的獨佔鎖定，但允許其他所有鎖定模式。 例如，SELECT 語句會起始共用鎖定，因此允許多個查詢同時存取選取的資料，但會防止更新讀取的記錄，直到 SELECT 語句完成為止。  
  
ExclusiveUpdate  
ExclusiveUpdate 鎖定會禁止寫入鎖定的物件，但允許透過共用鎖定來讀取。 ExclusiveUpdate 鎖定生效時，不允許任何其他鎖定。 例如，「備份資料庫」和「還原資料庫」使用獨佔更新鎖定。  
  
SharedUpdate  
SharedUpdate 鎖定會禁止獨佔和 ExclusiveUpdate 鎖定模式，並允許在物件上共用和 SharedUpdate 鎖定模式。 SharedUpdate 會修改物件，但不會在修改期間限制對它的讀取權限。 例如，INSERT 和 UPDATE 會使用 SharedUpdate 鎖定。  
  
**資源類別**  
  
鎖定會保留在下列物件類別中：資料庫、架構、物件（資料表、view 或 procedure）、應用程式（在內部使用）、EXTERNALDATASOURCE、EXTERNALFILEFORMAT 和 SCHEMARESOLUTION （建立、改變或時所採用的資料庫層級鎖定卸載架構物件或資料庫使用者）。 這些物件類別可以出現在[dm_pdw_waits sys.databases](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)的 object_type 資料行中。  
  
## <a name="Remarks"></a>一般備註  
鎖定可以套用至資料庫、資料表或 views。  
  
SQL Server PDW 不會執行任何可設定的隔離等級。 它支援 ANSI 標準所定義的 READ_UNCOMMITTED 隔離等級。 不過，由於讀取作業是在 READ_UNCOMMITTED 之下執行，因此非常少的封鎖作業實際上會發生或導致系統中的競爭。  
  
SQL Server PDW 依賴基礎 SQL Server 引擎來執行鎖定和並行控制。 如果作業導致相同節點內的基礎 SQL Server 鎖死，SQL Server PDW 會利用 SQL Server 的鎖死偵測功能，並終止其中一個封鎖語句。  
  
> [!NOTE]  
> SQL Server 不允許較新的鎖定要求封鎖等候鎖定的語句。 SQL Server PDW 尚未完全執行此程式。 在 SQL Server PDW 中，新共用鎖定的連續要求有時可能會封鎖上一個（但等候）獨佔鎖定的要求。 例如，針對**SELECT**語句的一系列授與的共用鎖定可能會封鎖**UPDATE**語句（需要獨佔鎖定）。 若要解決已封鎖的進程（藉由[dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)檢查 DVM），請停止提交新的要求，直到滿足獨佔鎖定為止。  
  
## <a name="lock-definition-table"></a>鎖定定義資料表  
SQL Server 支援下列鎖定類型。 並非所有的鎖定類型都可用於控制節點，但可能發生在計算節點上。  
  
-   .Sch-S （架構穩定性）。 確定在任何工作階段持有結構描述元素的結構描述穩定性鎖定時，不卸除結構描述元素，如資料表或索引。  
  
-   .Sch-M （架構修改）。 想要變更指定資源結構描述的任何工作階段都必須持有這個項目。 請確定沒有其他工作階段在參考指示的物件。  
  
-   S （共用）。 持有它的工作階段，會取得資源的共用存取權。  
  
-   U （更新）。 表示取得最終可能會更新之資源的更新鎖定。 它用來防止當多個工作階段為了未來可能更新資源而鎖定資源時，所常見的死結形式。  
  
-   X （獨佔）。 持有它的工作階段，會取得資源的獨佔存取權。  
  
-   IS （意圖共用）。 表示在鎖定階層中的某些從屬資源上設定 S 鎖定的意圖。  
  
-   IU （意圖更新）。 表示在鎖定階層中的某些從屬資源上設定 U 鎖定的意圖。  
  
-   IX （意圖獨佔）。 表示在鎖定階層中的某些從屬資源上設定 X 鎖定的意圖。  
  
-   SIU （共用意圖更新）。 表示意圖取得鎖定階層中從屬資源的更新鎖定之共用資源存取權。  
  
-   六（共用意圖獨佔）。 表示意圖取得鎖定階層中從屬資源的獨佔鎖定之共用資源存取權。  
  
-   UIX （Update 意圖獨佔）。 表示意圖取得鎖定階層中從屬資源的獨佔鎖定之資源更新鎖定。  
  
-   BU. 供大量作業使用。  
  
-   RangeS_S （共用索引鍵範圍和共用資源鎖定）。 指出可序列化的範圍掃描。  
  
-   RangeS_U （共用索引鍵範圍和更新資源鎖定）。 指出可序列化的更新掃描。  
  
-   RangeI_N （插入索引鍵範圍和 Null 資源鎖定）。 在將新索引鍵插入索引之前，用來測試範圍。  
  
-   RangeI_S。 索引鍵範圍轉換鎖定，由 RangeI_N 和 S 鎖定的重疊建立。  
  
-   RangeI_U。 索引鍵範圍轉換鎖定，由 RangeI_N 和 U 鎖定的重疊建立。  
  
-   RangeI_X。 索引鍵範圍轉換鎖定，由 RangeI_N 和 X 鎖定的重疊建立。  
  
-   RangeX_S。 索引鍵範圍轉換鎖定，由 RangeI_N 和 RangeS_S 鎖定的重疊建立 。  
  
-   RangeX_U。 索引鍵範圍轉換鎖定，由 RangeI_N 和 RangeS_U 鎖定的重疊建立。  
  
-   RangeX_X （獨佔索引鍵範圍和獨佔資源鎖定）。 這是更新範圍中的索引鍵時所用的轉換鎖定。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
