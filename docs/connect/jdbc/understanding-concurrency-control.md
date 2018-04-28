---
title: 瞭解並行控制 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98b7dabe-9b12-4e1d-adeb-e5b5cb0c96f3
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9a414c6d5fe2ee18fb83e168fe33fef53a0ac02c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="understanding-concurrency-control"></a>瞭解並行控制
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  並行控制意指多個使用者同時更新資料列時，用於保留資料庫完整性的各種技術。 並行不正確可能導致的問題包括中途讀取、虛設項目讀取，以及不可重複讀取。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供介面給所使用的所有並行技術[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]來解決這些問題。  
  
> [!NOTE]  
>  如需有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的並行存取，請參閱中的 < 管理並行資料存取 >[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="remarks"></a>備註  
 JDBC 驅動程式支援下列並行類型：  
  
|並行類型|特性|資料列鎖定|Description|  
|----------------------|---------------------|---------------|-----------------|  
|CONCUR_READ_ONLY|唯讀|否|不允許透過資料指標進行更新，且構成結果集之資料列中不保留鎖定。|  
|CONCUR_UPDATABLE|開放式讀寫|否|資料庫假設未必會發生資料列競爭，但是有可能。 資料列的完整性會透過時間戳記比較來確認。|  
|CONCUR_SS_SCROLL_LOCKS|封閉式 (Pessimistic) 讀寫|是|資料庫假設可能會發生資料列競爭。 資料列的完整性會透過資料列鎖定來確保。|  
|CONCUR_SS_OPTIMISTIC_CC|開放式讀寫|否|資料庫假設未必會發生資料列競爭，但是有可能。 資料列的完整性會透過時間戳記比較來確認。<br /><br /> 如[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]和更新版本中，伺服器將會變更為 CONCUR_SS_OPTIMISTIC_CCVAL 如果資料表不包含時間戳記資料行。<br /><br /> 如[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]，即使指定 OPTIMISTIC WITH VALUES，如果基礎資料表有時間戳記資料行，會使用 OPTIMISTIC WITH ROW VERSIONING。 如果指定了 OPTIMISTIC WITH ROW VERSIONING，且資料表沒有時間戳記，就會使用 OPTIMISTIC WITH VALUES。|  
|CONCUR_SS_OPTIMISTIC_CCVAL|開放式讀寫|否|資料庫假設未必會發生資料列競爭，但是有可能。 資料列的完整性會透過資料列資料比較來確認。|  
  
## <a name="result-sets-that-are-not-updateable"></a>不可更新的結果集  
 可更新的結果集是可以在其中插入、更新和刪除的資料集。 在下列情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]無法建立可更新的資料指標。 產生的例外狀況為：「結果集無法更新。」。  
  
|原因|Description|補救方法|  
|-----------|-----------------|------------|  
|使用 JDBC 2.0 (或更新版本) 語法沒有建立陳述式|JDBC 2.0 推出建立陳述式的新方法。 如果使用 JDBC 1.0 語法，結果集預設為唯讀。|建立陳述式時，指定結果集類型與並行。|  
|使用 TYPE_SCROLL_INSENSITIVE 建立陳述式|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 建立靜態快照集資料指標。 這會與基礎資料表資料列中斷連接，以防資料指標遭到其他使用者更新資料列。|搭配 CONCUR_UPDATABLE 使用 TYPE_SCROLL_SENSITIVE、TYPE_SS_SCROLL_KEYSET、TYPE_SS_SCROLL_DYNAMIC 或 TYPE_FORWARD_ONLY 以防建立靜態資料指標。|  
|資料表設計會避開 KEYSET 或 DYNAMIC 資料指標|基礎資料表沒有唯一索引鍵，讓[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]來唯一識別資料列。|將唯一的索引鍵加入到資料表中即可提供每個資料列的唯一識別。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 JDBC Driver 管理結果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
