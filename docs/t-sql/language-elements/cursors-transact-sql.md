---
title: "資料指標 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], cursors
- functions [SQL Server], cursors
- cursors [SQL Server], statements
ms.assetid: 63000023-54fc-4efc-a30f-fb4d4db73aae
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 990b1bc3c44605e2b7debed67b88e5cd65770ed5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="cursors-transact-sql"></a>資料指標 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]陳述式會產生完整的結果集，但是有的時間結果適合一次處理一個資料列。 您可以在結果集上開啟一個資料指標，一次處理一個資料列結果集。 您可以將資料指標指派給變數或參數**游標**資料型別。  
  
 下列陳述式皆支援資料指標作業：  
  
 [關閉](../../t-sql/language-elements/close-transact-sql.md)  
  
 [CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)  
  
 [解除配置](../../t-sql/language-elements/deallocate-transact-sql.md)  
  
 [宣告資料指標](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
  
 [DECLARE@local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [擷取](../../t-sql/language-elements/fetch-transact-sql.md)  
  
 [開啟](../../t-sql/language-elements/open-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [設定](../../t-sql/statements/set-statements-transact-sql.md)  
  
 這些系統函數和系統預存程序也支援資料指標：  
  
 [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)  
  
 [CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)  
  
 [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)  
  
 [sp_cursor_list](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)  
  
 [sp_describe_cursor](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)  
  
 [sp_describe_cursor_columns](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)  
  
 [sp_describe_cursor_tables](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料指標](../../relational-databases/cursors.md)  
  
  

