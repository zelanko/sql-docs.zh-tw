---
title: "提示 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6d2d8b50a38299162677b1f7d5bbff501fba9881
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="hints-transact-sql"></a>提示 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  提示是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢處理器在 SELECT、INSERT、UPDATE 或 DELETE 陳述式指定要強制執行的選項或策略。 提示會覆寫任何查詢最佳化工具可能會針對查詢而選取的執行計畫。  
  
> [!CAUTION]  
>  因為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查詢最佳化工具通常會選取查詢的最佳執行計畫，所以建議\<join_hint >， \<query_hint >，並\<table_hint > 只能做為最後的手段使用由有經驗開發人員和資料庫管理員。
  
 此章節將描述下列提示：  
  
-   [聯結提示](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [資料表提示](../../t-sql/queries/hints-transact-sql-table.md)  
  
  

