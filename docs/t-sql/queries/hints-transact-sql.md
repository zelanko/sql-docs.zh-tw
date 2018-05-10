---
title: 提示 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query optimizer [SQL Server], hints
- hints [SQL Server], about hints
- SELECT statement [SQL Server], hints
- hints [SQL Server]
- INSERT statement [SQL Server], hints
- UPDATE statement [SQL Server], hints
- DELETE statement [SQL Server], hints
ms.assetid: 99412475-b0df-4264-9938-33a0b302b41a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a404f015c177fe38985c07470645e9a16e2cb716
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="hints-transact-sql"></a>提示 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  提示是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢處理器在 SELECT、INSERT、UPDATE 或 DELETE 陳述式指定要強制執行的選項或策略。 提示會覆寫任何查詢最佳化工具可能會針對查詢而選取的執行計畫。  
  
> [!CAUTION]  
>  由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具通常會選取最佳的查詢執行計劃，因此建議資深開發人員和資料庫管理員只有在別無他法時，才使用 \<join_hint>、\<query_hint> 及 \<table_hint>。
  
 此章節將描述下列提示：  
  
-   [聯結提示](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [資料表提示](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
