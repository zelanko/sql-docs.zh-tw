---
title: 了解並行存取控制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 98b7dabe-9b12-4e1d-adeb-e5b5cb0c96f3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35d62927e8f7579c207ddaa4cd5c7fe04a4cd3f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654346"
---
# <a name="understanding-concurrency-control"></a>瞭解並行控制
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  並行控制意指多個使用者同時更新資料列時，用於保留資料庫完整性的各種技術。 並行不正確可能導致的問題包括中途讀取、虛設項目讀取，以及不可重複讀取。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供介面給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所使用的所有並行技術來解決這些問題。  
  
> [!NOTE]  
>  如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並行的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜管理並行資料存取＞。  
  
## <a name="remarks"></a>Remarks  
 JDBC 驅動程式支援下列並行類型：  
  
|並行類型|特性|資料列鎖定|Description|  
|----------------------|---------------------|---------------|-----------------|  
|CONCUR_READ_ONLY|唯讀|否|不允許透過資料指標進行更新，且構成結果集之資料列中不保留鎖定。|  
|CONCUR_UPDATABLE|開放式讀寫|否|資料庫假設未必會發生資料列競爭，但是有可能。 資料列的完整性會透過時間戳記比較來確認。|  
|CONCUR_SS_SCROLL_LOCKS|封閉式 (Pessimistic) 讀寫|是|資料庫假設可能會發生資料列競爭。 資料列的完整性會透過資料列鎖定來確保。|  
|CONCUR_SS_OPTIMISTIC_CC|開放式讀寫|否|資料庫假設未必會發生資料列競爭，但是有可能。 資料列的完整性會透過時間戳記比較來確認。<br /><br /> 如果是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本，且資料表不包含時間戳記資料行，伺服器會將其變更為 CONCUR_SS_OPTIMISTIC_CCVAL。<br /><br /> 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，如果基礎資料表有時間戳記資料行，即使有指定 OPTIMISTIC WITH VALUES，也會使用 OPTIMISTIC WITH ROW VERSIONING。 如果指定了 OPTIMISTIC WITH ROW VERSIONING，且資料表沒有時間戳記，就會使用 OPTIMISTIC WITH VALUES。|  
|CONCUR_SS_OPTIMISTIC_CCVAL|開放式讀寫|否|資料庫假設未必會發生資料列競爭，但是有可能。 資料列的完整性會透過資料列資料比較來確認。|  
  
## <a name="result-sets-that-are-not-updateable"></a>不可更新的結果集  
 可更新的結果集是可以在其中插入、更新和刪除的資料集。 在下列情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法建立可更新的資料指標。 產生的例外狀況為：「結果集無法更新。」。  
  
|原因|Description|補救方法|  
|-----------|-----------------|------------|  
|使用 JDBC 2.0 (或更新版本) 語法沒有建立陳述式|JDBC 2.0 推出建立陳述式的新方法。 如果使用 JDBC 1.0 語法，結果集預設為唯讀。|建立陳述式時，指定結果集類型與並行。|  
|使用 TYPE_SCROLL_INSENSITIVE 建立陳述式|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會建立靜態快照集資料指標。 這會與基礎資料表資料列中斷連接，以防資料指標遭到其他使用者更新資料列。|搭配 CONCUR_UPDATABLE 使用 TYPE_SCROLL_SENSITIVE、TYPE_SS_SCROLL_KEYSET、TYPE_SS_SCROLL_DYNAMIC 或 TYPE_FORWARD_ONLY 以防建立靜態資料指標。|  
|資料表設計會避開 KEYSET 或 DYNAMIC 資料指標|基礎資料表沒有唯一的索引鍵，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 唯一識別資料列。|將唯一的索引鍵加入到資料表中即可提供每個資料列的唯一識別。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 JDBC Driver 管理結果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
