---
title: 使用快照集初始化訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 03/23/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bb09b6d532e6b7db7310e0d375609665d9c45db5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "80216007"
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>使用快照集初始化訂閱

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

本文描述初始化複寫發行集時所發生的處理。 初始快照集會套用至訂閱者。

## <a name="snapshot-for-a-new-publication"></a>新發行集的快照集

預設會在建立發行集之後擷取快照集。
快照集會複製到快照集資料夾。 使用 [新增發行集精靈] 所建立的合併式發行集，會發生這種預設行為。

### <a name="snapshot-is-applied-to-subscriber"></a>快照集套用至訂閱者

代理程式會將新的快照集套用至訂閱者。 套用會在訂閱的初始同步處理期間進行。 執行套用的代理程式取決於發行集類型而定：

- 若為「交易式」  發行集和「快照式」  發行集：
  - 散發代理程式。

- 若為「合併式」  發行集：
  - 合併代理程式。

### <a name="type-of-publication"></a>發行集的類型

下表顯示每種發行集類型的快照集內容。

&nbsp;

| 快照集所屬發行集類型 | 快照集的內容 |
| :---------------------------------------- | :----------------------- |
| <ul> <li>快照式發行集</li> <li>交易式發行集</li> <li>不使用參數化篩選的合併式發行集</li> </ul> | <ul> <li>結構描述</li> <li>資料 (位在大量複製程式 (BCP) 的檔案中)</li> <li>條件約束</li> <li>擴充屬性</li> <li>索引</li> <li>觸發程序</li> <li>複寫所需的系統資料表</li> </ul> <br/>請參閱[建立並套用快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。 |
| <ul> <li>使用參數化篩選的合併式發行集</li> </ul> | <ul> <li>結構描述快照集 (複寫指令碼、已發佈的物件，但沒有資料)</li> <li>屬於訂閱分割區的資料</li> </ul> <br/>請參閱[適用於合併式發行集 (含參數化篩選) 的快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。 |
| | |

#### <a name="two-part-process-with-merge-publication-that-uses-parameterized-filters"></a>合併式發行集 (使用參數化篩選) 的兩部分處理

針對使用參數化篩選的合併式發行集，則會使用下列兩部分處理來建立快照集：

1. 建立結構描述快照集，其中包含下列項目：
   - 複寫指令碼。
   - 已發佈物件的結構描述。
   - (但沒有資料。) 

2. 接著使用快照集來初始化每個訂閱。 快照集包含下列各項：
   - 指令碼和結構描述 (從結構描述快照集複製而來)。
   - 屬於訂閱分割區的資料。

## <a name="type-of-replication"></a>複寫類型

快照集所包含的檔案類型取決於複寫類型，以及發行集中的發行項。

&nbsp;

| 複寫類型 | 一般快照集檔 |
| :------------------ | :-------------------- |
| 快照式複寫，或<br/>異動複寫 | &bullet; 結構描述 (.sch) <br/>&bullet; 資料 (.bcp) <br/>&bullet; 條件約束和索引 (.dri) <br/>&bullet; 壓縮的快照集檔案 (.cab) <br/>&bullet; 觸發程序 (.tag)，僅用於更新訂閱者 <br/><br/>&bullet; 條件約束 (.idx)。 |
| 合併式複寫                                      | &bullet; 結構描述 (.sch) <br/>&bullet; 資料 (.bcp) <br/>&bullet; 條件約束和索引 (.dri) <br/>&bullet; 壓縮的快照集檔案 (.cab) <br/>&bullet; 觸發程序 (.trg) <br/><br/>&bullet; 系統資料表資料 (.sys) <br/>&bullet; 衝突資料表 (.cft)。 |
| | |

### <a name="snapshot-folder"></a>快照集資料夾

這些檔案會透過複製到預設的「快照集資料夾」  或快照集的「替代資料夾」  來傳輸。

當設定散發者時，會指定快照集資料夾。 建立發行集時，則會指定替代資料夾。

### <a name="resume-transfer-after-interruption"></a>中斷之後繼續傳輸

如果傳輸是因不可靠的連線而中斷，則會自動繼續將檔案傳輸至快照集資料夾。

為了提高效率，繼續動作不會重新傳送中斷前已完全傳輸的任何檔案。

## <a name="snapshot-options"></a>快照集選項

使用快照集初始化訂閱時，可以使用下列幾個選項。 您可以：

- 指定代替預設快照集資料夾位置的替代快照集資料夾位置，或同時指定這兩個位置。 如需詳細資訊，請參閱 [修改快照集選項](../../relational-databases/replication/snapshot-options.md)。

- 壓縮快照集以儲存在抽取式媒體，或者透過慢速網路傳送。 如需詳細資訊，請參閱＜ [Compressed Snapshots](../../relational-databases/replication/snapshot-options.md#compressed-snapshots)＞。

- 在套用快照集之前及之後執行 Transact-SQL 指令碼。 如需詳細資訊，請參閱[在套用快照集之前及之後執行指令碼](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)。

- 使用檔案傳輸通訊協定 (FTP) 傳送快照集檔案。 如需詳細資訊，請參閱[透過 FTP 傳送快照集](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)。

## <a name="see-also"></a>另請參閱

[初始化訂閱](../../relational-databases/replication/initialize-a-subscription.md)

[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)
