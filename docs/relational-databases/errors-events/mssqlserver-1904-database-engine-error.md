---
title: MSSQLSERVER_1904 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1904 (Database Engine error)
ms.assetid: 2a35d57d-74e2-45a2-8f67-3f2e51d69712
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7f40d48806c181cc12c804bfa5fdf9796f83b77e
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver1904"></a>MSSQLSERVER_1904
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1904|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|KEYCOUNT|  
|訊息文字|資料表 '%.\*ls' 上的 %S_MSG '%.*ls'，其在 %S_MSG 索引鍵清單中有 %d 個資料行名稱。 索引或統計資料索引鍵資料行清單的上限為 %d。|  
  
## <a name="explanation"></a>說明  
指定之索引或統計資料的索引鍵資料行清單超過允許的資料行數目上限。  
  
## <a name="user-action"></a>使用者動作  
將索引鍵資料行清單修改成包含不超過指定的資料行數目上限。  
  
若為非叢集索引，請考慮在 CREATE INDEX 陳述式中使用 INCLUDE 子句，以便將資料行加入至索引，當做非索引鍵資料行。 這個方法可避免超過目前索引大小限制：16 個索引鍵資料行的上限。 如需詳細資訊，請參閱 [建立內含資料行的索引](~/relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
## <a name="see-also"></a>另請參閱  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[CREATE STATISTICS &#40;Transact-SQL&#41;](~/t-sql/statements/create-statistics-transact-sql.md)  
  

