---
title: 鎖定行為-Parallel Data Warehouse |Microsoft Docs
description: 了解如何平行處理資料倉儲會使用鎖定來確保交易完整性，並當多位使用者同時存取資料，同時維護資料庫一致性。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d93743c83d6315e6ab9484445f344b06f80be845
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960648"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>在平行處理資料倉儲中的鎖定行為
了解如何平行處理資料倉儲會使用鎖定來確保交易完整性，並當多位使用者同時存取資料，同時維護資料庫一致性。  
  
## <a name="Basics"></a>鎖定的基本概念  
**模式**  
  
SQL Server PDW 支援四種鎖定模式：  
  
排除  
寫入或讀取鎖定的物件，直到交易持有獨佔鎖定完成，則會禁止的獨佔鎖定。 獨佔鎖定是作用中時，會不允許任何模式的任何其他鎖定。 比方說，DROP TABLE 和 CREATE DATABASE 使用的獨佔鎖定。  
  
共用  
共用鎖定禁止初始的受影響的物件的獨佔鎖定，但可讓所有其他鎖定模式。 比方說，SELECT 陳述式起始共用鎖定，因此可讓多個查詢，同時也會存取選取的資料但會阻止讀取，SELECT 陳述式完成之前的記錄更新。  
  
ExclusiveUpdate  
ExclusiveUpdate 鎖定禁止寫入鎖定的物件，但允許透過共用鎖定的讀取。 ExclusiveUpdate 鎖定生效時，會不允許任何其他鎖定。 比方說，BACKUP DATABASE 和 RESTORE DATABASE 使用的專屬的更新鎖定。  
  
SharedUpdate  
SharedUpdate 鎖定禁止獨佔和 ExclusiveUpdate 鎖定模式，並允許在物件上的共用和 SharedUpdate 鎖定模式。 SharedUpdate 修改物件，但不會限制在修改期間進行的讀取權限。 例如，插入和更新使用的 SharedUpdate 鎖定。  
  
**資源類別**  
  
保留鎖定之物件的下列類別：資料庫、 結構描述、 物件 （資料表、 檢視或程序）、 應用程式 （在內部使用）、 EXTERNALDATASOURCE，EXTERNALFILEFORMAT 和 SCHEMARESOLUTION （資料庫層級鎖定時建立、 改變或卸除結構描述物件或資料庫使用者）。 這些物件類別可以 object_type 資料行中出現[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)。  
  
## <a name="Remarks"></a>一般備註  
鎖定可以套用至資料庫、 資料表或檢視中。  
  
SQL Server PDW 不會實作任何可設定的隔離等級。 ANSI 標準所定義，它就會支援能在 READ_UNCOMMITTED 隔離等級。 不過，讀取作業能在 READ_UNCOMMITTED 下執行，因為很少的封鎖作業實際上發生或導致爭用系統中。  
  
SQL Server PDW 依賴基礎 SQL Server 引擎實作鎖定和並行存取控制。 如果作業會導致在相同節點基礎 SQL Server 發生死結，SQL Server PDW 運用 SQL Server 的死結偵測功能，並終止其中一個封鎖的陳述式。  
  
> [!NOTE]  
> SQL Server 不允許陳述式，會等候到較新的鎖定要求遭到封鎖的鎖定。 SQL Server PDW 尚未完全實作此程序。 在 SQL Server PDW 中，新的共用鎖定的連續要求有時候可能會封鎖的獨佔鎖定的上一個 （但等候） 要求。 例如，**更新**陳述式 （需要獨佔鎖定） 可能會封鎖所授與一系列的共用鎖定**選取**陳述式。 若要解決已封鎖的處理序 (藉由檢閱識別[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM)，停止送出新的要求，直到已滿足的獨佔鎖定。  
  
## <a name="lock-definition-table"></a>鎖定定義資料表  
SQL Server 支援下列類型的鎖定。 並非所有的鎖定類型的控制節點上可用，但可能發生的計算節點上。  
  
-   Sch-s （結構描述穩定性）。 確定在任何工作階段持有結構描述元素的結構描述穩定性鎖定時，不卸除結構描述元素，如資料表或索引。  
  
-   Sch-m （結構描述修改）。 想要變更指定資源結構描述的任何工作階段都必須持有這個項目。 請確定沒有其他工作階段在參考指示的物件。  
  
-   S （共用）。 持有它的工作階段，會取得資源的共用存取權。  
  
-   U （更新）。 表示取得最終可能會更新之資源的更新鎖定。 它用來防止當多個工作階段為了未來可能更新資源而鎖定資源時，所常見的死結形式。  
  
-   X （獨佔）。 持有它的工作階段，會取得資源的獨佔存取權。  
  
-   IS （意圖共用）。 表示在鎖定階層中的某些從屬資源上設定 S 鎖定的意圖。  
  
-   IU （意圖更新）。 表示在鎖定階層中的某些從屬資源上設定 U 鎖定的意圖。  
  
-   IX （意圖獨佔）。 表示在鎖定階層中的某些從屬資源上設定 X 鎖定的意圖。  
  
-   SIU （共用意圖更新）。 表示意圖取得鎖定階層中從屬資源的更新鎖定之共用資源存取權。  
  
-   六個 （共用意圖獨佔）。 表示意圖取得鎖定階層中從屬資源的獨佔鎖定之共用資源存取權。  
  
-   UIX （更新意圖獨佔）。 表示意圖取得鎖定階層中從屬資源的獨佔鎖定之資源更新鎖定。  
  
-   BU。 供大量作業使用。  
  
-   RangeS_S （共用索引鍵範圍和共用資源鎖定）。 指出可序列化的範圍掃描。  
  
-   RangeS_U （共用索引鍵範圍和更新資源鎖定）。 指出可序列化的更新掃描。  
  
-   RangeI_N （插入的索引鍵範圍和 Null 資源鎖定）。 在將新索引鍵插入索引之前，用來測試範圍。  
  
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
  
