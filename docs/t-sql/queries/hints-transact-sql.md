---
description: 提示 (Transact-SQL)
title: 提示 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 16f0e437e864ccb2bd0b4c173b40d84098c51b30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459176"
---
# <a name="hints-transact-sql"></a>提示 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  提示是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢處理器在 SELECT、INSERT、UPDATE 或 DELETE 陳述式指定要強制執行的選項或策略。 提示會覆寫任何查詢最佳化工具可能會針對查詢而選取的執行計畫。  
  
> [!CAUTION]  
>  由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具通常會選取最好的查詢執行計畫，因此我們建議只有資深的開發人員和資料庫管理員才應該使用 \<join_hint>、\<query_hint> 和 \<table_hint>，並將其當作最後的解決辦法。
  
 此章節將描述下列提示：  
  
-   [聯結提示](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [資料表提示](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
