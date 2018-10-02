---
title: 完成 Transact-SQL 程式碼片段 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], completing snippets
- snippets [Transact-SQL], completing
- Transact-SQL snippets, completing
ms.assetid: a8316a58-bb57-485e-845f-84c23360314c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6326830107d04e2706ab159bd87737915be50944
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650596"
---
# <a name="complete-transact-sql-snippets"></a>完成 Transact-SQL 程式碼片段
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  一旦您已經將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼片段插入指令碼之後，就可以編輯片段的內容，以便建立完整的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
## <a name="completing-snippets"></a>完成片段  
 當您將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 片段加入至指令碼時，已插入的片段陳述式就會具有一個或多個反白顯示的取代點。 如果您將滑鼠指標停留在取代點上方，就會顯示工具提示，其中說明您可以指定的語法元素。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器會將該片段視為不同於周圍的指令碼，直到您關閉來源檔案為止。 此外，取代點會維持作用中狀態，直到您關閉來源檔案為止。  
  
 您也可以將其他語法元素加入至片段所插入的範本程式碼。 例如，「建立資料表」片段範本會產生兩個資料行定義。您必須加入其他資料行定義，以便建立具有兩個以上資料行的資料表。  
  
#### <a name="completing-the-snippet-statement"></a>完成片段陳述式  
  
1.  您可以使用 TAB 鍵，從某個取代點移至下一個取代點。 您可以使用 SHIFT+TAB，移至上一個取代點。  
  
2.  按一下 CTRL+SPACE 叫用 IntelliSense。  
  
3.  從清單中選取項目，或輸入您選擇的取代項目。  
  
## <a name="see-also"></a>另請參閱  
 [插入 Transact-SQL 程式碼片段](../../relational-databases/scripting/insert-transact-sql-snippets.md)   
 [插入範圍陳述式 Transact-SQL 程式碼片段](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
