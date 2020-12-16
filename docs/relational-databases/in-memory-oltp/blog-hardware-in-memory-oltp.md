---
title: SQL In-Memory OLTP 的硬體 | Microsoft Docs
description: 了解 SQL Server 中記憶體內部 OLTP 效能的硬體考量事項。 記憶體內部 OLTP 使用記憶體和磁碟其方式與以磁碟為基礎的資料表不同。
ms.custom: ''
ms.date: 03/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017
ms.openlocfilehash: 09483122764de51b565693d85c3ae8efa9a8c570
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465349"
---
# <a name="hardware-considerations-for-in-memory-oltp-in-sql-server"></a>SQL Server 中記憶體內部 OLTP 的硬體考量

In-Memory OLTP 會以不同於傳統磁碟資料表的方式，使用記憶體和磁碟。 您將會看到使用 In-Memory OLTP 提升的效能取決於您所使用的硬體。 在此部落格文章中，我們會討論一些一般硬體考量，並針對搭配 In-Memory OLTP 使用的硬體，提供常用的指導方針。

> [!NOTE]
> 本文已在 2013 年 8 月 1 日，由 Microsoft SQL Server 2014 小組發佈在部落格上。 即將淘汰的部落格網頁。
>
> [SQL Server In-Memory-OLTP](./in-memory-oltp-in-memory-optimization.md)

<!--
    Here was the link to the blog. This blog was captured into this new article on 2018/11/30, by GeneMi (MightyPen).
    https://cloudblogs.microsoft.com/sqlserver/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014/
    At least one pre-existing article that contained the obsolete blog link was:
        relational-databases\in-memory-oltp\sample-database-for-in-memory-oltp.md
-->

## <a name="cpu"></a>CPU

In-Memory OLTP 不需要高階的伺服器，就可以支援高輸送量的 OLTP 工作負載。 我們建議使用含有 2 個 CPU 插槽的中型伺服器。 由於 In-Memory OLTP 允許的輸送量不斷增加，2 個通訊端對於您的業務需求可能就已經足夠。

我們建議使用 In-Memory OLTP 開啟超執行緒。 對於部分 OLTP 工作負載，使用超執行緒時，我們看到效能提升高達 40%。

## <a name="memory"></a>記憶體

所有記憶體最佳化資料表都完全位於記憶體中。 因此，您必須擁有足夠的實體記憶體供資料表本身使用，並維持對資料庫執行的工作負載。您實際上需要的記憶體數量事實上取決於工作負載，但您可能需要足夠的可用記憶體供大約 2 倍的資料大小，作為起點。 您也需要足夠的記憶體供緩衝集區使用，以免工作負載也在傳統磁碟資料表上運作。

若要判斷指定的記憶體最佳化資料表所使用的記憶體數量，請執行下列查詢：

```sql
select object_name(object_id), * from sys.dm_db_xtp_table_memory_stats;
```

結果將會顯示用於記憶體最佳化資料表及其索引的記憶體。 資料表資料包括使用者資料，以及執行交易仍然需要，或者系統尚未清除的所有舊版資料列。 雜湊索引所使用的記憶體為常數，而且不取決於資料表中的資料列數目。

請務必請記住，當您使用 In-Memory OLTP 時，整個資料庫都不需要納入記憶體中。 您可以擁有好幾 TB 的資料庫，而且仍然受益於 In-Memory OLTP，但前提是您常用資料 (亦即，記憶體最佳化資料表) 的大小不超過 256GB。 SQL Server 可以為單一資料庫管理的檢查點資料檔案數目上限為 4000 個檔案，而且每個檔案大小都是 128MB。 理論上的最大值為 512GB，但是為了保證 SQL Server 可以跟上合併檢查點檔案，而且不會達到 4000 個檔案的限制，我們支援最多 256GB。 請注意，此限制僅適用於記憶體最佳化資料表；傳統磁碟資料表在相同的 SQL Server 資料庫中則沒有這類大小限制。

非持久性記憶體最佳化資料表 (NDT)，也就是 DURABILITY=SCHEMA_ONLY 的記憶體最佳化資料表，並不會保存在磁碟上。 雖然 NDT 不會受到檢查點檔案數目的限制，但只會支援 256GB。 本文其餘部分的記錄檔和資料磁碟機考量不適用於非持久性資料表，因為資料只存在於記憶體中。

## <a name="log-drive"></a>記錄磁碟機

有關記憶體最佳化資料表的記錄檔記錄以及其他 SQL Server 記錄檔記錄會寫入資料庫交易記錄檔。

請務必一律將記錄檔放在具有低延遲的磁碟機上，讓交易不需要等候太久，並避免爭用記錄 IO。 您的系統將會與您最慢的元件 (阿姆達爾定律) 執行得一樣快。 您需要確保在執行 In-Memory OLTP 時，您的記錄 IO 裝置不會成為瓶頸。 建議使用具有低延遲的儲存裝置，至少是 SSD。

請注意，記憶體最佳化資料表使用的記錄檔頻寬比以磁碟資料表少，因為它們不會記錄索引作業，而且不會記錄 UNDO 記錄。 這有助於減輕記錄 IO 爭用。

## <a name="data-drive"></a>資料磁碟機

使用檢查點檔案的記憶體最佳化資料表持續性會使用串流 IO。 因此，這些檔案不需要具有低延遲或快速隨機 IO 的磁碟機。 但是，這些磁碟機的主要因素是連續 IO 的速度以及主機匯流排介面卡 (HBA) 的頻寬。 因此，您不需要為檢查點檔案使用 SSD；您可以將這些檔案放在高效能讀寫頭上 (例如 SAS)，但前提是，其連續 IO 速度符合您的需求。

判斷速度需求的最大要素是伺服器重新啟動時的 RTO [復原時間目標]。 在資料庫復原期間，記憶體最佳化資料表中的所有資料都必須從磁碟讀入記憶體中。 資料庫復原會以 IO 子系統的連續讀取速度進行；磁碟是瓶頸。

若要滿足嚴苛的 RTO 需求，建議將檢查點檔案分散在多個磁碟中，方法是，將多個容器加入至 MEMORY_OPTIMIZED_DATA 檔案群組。 SQL Server 支援從多個磁碟機平行載入檢查點檔案，復原會以磁碟機的彙總速度進行。

磁碟容量方面，我們建議具備 2 到 3 倍的可用記憶體最佳化資料表大小。

## <a name="see-also"></a>另請參閱

[記憶體內部 OLTP 的範例資料庫](sample-database-for-in-memory-oltp.md)