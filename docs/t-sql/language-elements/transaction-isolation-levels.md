---
title: "交易隔離等級 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.openlocfilehash: 7f13bd2886aaf2363cde83461f246bf034c89de5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="transaction-isolation-levels"></a>交易隔離等級
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不保證在透過目錄檢視、相容性檢視、資訊結構描述檢視，以及發出中繼資料之內建函數來存取中繼資料的查詢中，一定能夠接受鎖定提示。  
  
 就內部而言，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 只接受中繼資料存取的 READ COMMITTED 隔離等級。 例如，如果某交易的隔離等級為 SERIALIZABLE，且交易中試圖以目錄檢視或發出中繼資料的內建函數來存取中繼資料，這些查詢會持續執行到其成為 READ COMMITTED 為止。 但在快照隔離下，對中繼資料的存取可能會因並行的 DDL 作業而失敗。 這是因為中繼資料並未建立版本。 因此，在快照隔離下存取下列項目可能會失敗：  
  
-   目錄檢視  
  
-   相容性檢視  
  
-   資訊結構描述檢視  
  
-   發出中繼資料的內建函數  
  
-   **sp_help**群組中的預存程序  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 目錄程序  
  
-   動態管理檢視與函數  
  
 如需有關隔離等級的詳細資訊，請參閱[SET TRANSACTION ISOLATION LEVEL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 下表提供在各種隔離等級下存取中繼資料的摘要。  
  
|隔離等級|支援|接受|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|否|不保證|  
|READ COMMITTED|是|是|  
|REPEATABLE READ|否|否|  
|SNAPSHOT ISOLATION|否|否|  
|SERIALIZABLE|否|否|  
  
  
