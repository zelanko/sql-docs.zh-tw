---
title: 完成 Transact-SQL 程式碼片段 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], completing snippets
- snippets [Transact-SQL], completing
- Transact-SQL snippets, completing
ms.assetid: a8316a58-bb57-485e-845f-84c23360314c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 103b8c23dba7119dde28a8d6e87b963400eaf0c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090590"
---
# <a name="complete-transact-sql-snippets"></a>完成 Transact-SQL 程式碼片段
  一旦您已經將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼片段插入指令碼之後，就可以編輯片段的內容，以便建立完整的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
## <a name="completing-snippets"></a>完成片段  
 當您將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 片段加入至指令碼時，已插入的片段陳述式就會具有一個或多個反白顯示的取代點。 如果您將滑鼠指標停留在取代點上方，就會顯示工具提示，其中說明您可以指定的語法元素。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器會將該片段視為不同於周圍的指令碼，直到您關閉來源檔案為止。 此外，取代點會維持作用中狀態，直到您關閉來源檔案為止。  
  
 您也可以將其他語法元素加入至片段所插入的範本程式碼。 例如，「建立資料表」片段範本會產生兩個資料行定義。您必須加入其他資料行定義，以便建立具有兩個以上資料行的資料表。  
  
#### <a name="completing-the-snippet-statement"></a>完成片段陳述式  
  
1.  您可以使用 TAB 鍵，從某個取代點移至下一個取代點。 您可以使用 SHIFT+TAB，移至上一個取代點。  
  
2.  按一下 CTRL+SPACE 叫用 IntelliSense。  
  
3.  從清單中選取項目，或輸入您選擇的取代項目。  
  
## <a name="see-also"></a>另請參閱  
 [插入 Transact-SQL 程式碼片段](insert-transact-sql-snippets.md)   
 [插入範圍陳述式 Transact-SQL 程式碼片段](insert-surround-with-transact-sql-snippets.md)  
  
  
