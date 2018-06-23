---
title: MSSQLSERVER_2530 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
caps.latest.revision: 11
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ccf0b157984cce59ceff84fcff0c25a2f708e26f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145631"
---
# <a name="mssqlserver2530"></a>MSSQLSERVER_2530
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|2530|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_INDEX_IS_OFFLINE|  
|訊息文字|資料表 "%.\*ls" 上的索引 "%.*ls" 已停用。|  
  
## <a name="explanation"></a>說明  
 指定的索引已停用，因此無法進行 SQL 陳述式。 索引停用後，在重建或卸除並重新建立之前，索引會一直維持在停用狀態。  
  
## <a name="user-action"></a>使用者動作  
  
1.  使用以下其中一個方法來啟用已停用的索引：  
  
    -   ALTER INDEX 陳述式加上 REBUILD 子句  
  
    -   CREATE INDEX 加上 DROP_EXISTING 子句  
  
    -   DBCC DBREINDEX  
  
2.  請重新執行 DBCC 陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [啟用索引與條件約束](../indexes/enable-indexes-and-constraints.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)  
  
  
