---
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b27694f791e29aa812ee4e2b52ecb3d17901e482
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3961"></a>MSSQLSERVER_3961
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|3961|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|XACT_METADATA_INVALID|  
|訊息文字|資料庫 '%.*ls' 中的快照集隔離交易失敗，因為這個交易啟動之後，另一個並行交易的 DDL 陳述式修改了此陳述式存取的物件。  這是不允許的，因為中繼資料並未建立版本。 如果在快照集隔離下並行更新中繼資料，將會造成不一致的問題。|  
  
## <a name="explanation"></a>說明  
如果您要查詢快照隔離下的中繼資料，而且有並行 DDL 陳述式可更新在快照隔離下存取的中繼資料，就可能會發生這個錯誤。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援中繼資料的版本控制。 因此，哪些 DDL 作業可以在快照隔離之下執行的明確交易中執行會有一些限制。 就定義而言，隱含交易是一種單一陳述式，可強制使用快照隔離的語意 (即使是 DDL 陳述式)。 快照隔離之下的 BEGIN TRANSACTION 陳述式之後不允許有下列 DDL 陳述式：ALTER TABLE、CREATE INDEX、CREATE XML INDEX、ALTER INDEX、DROP INDEX、DBCC REINDEX、ALTER PARTITION FUNCTION、ALTER PARTITION SCHEME 或是任何 Common Language Runtime (CLR) DDL 陳述式。 當您在隱含交易內使用快照隔離時，便允許這些陳述式。 就定義而言，隱含交易是一種單一陳述式，可強制使用快照隔離的語意 (即使是 DDL 陳述式)。  
  
## <a name="user-action"></a>使用者動作  
將快照隔離等級變更為非快照隔離等級，例如在查詢中繼資料之前認可的讀取。  
  
