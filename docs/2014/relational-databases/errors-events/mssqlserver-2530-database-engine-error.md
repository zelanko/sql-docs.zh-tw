---
title: MSSQLSERVER_2530 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1bb321f89c70983855e00b3eec4382c51fce1e16
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552047"
---
# <a name="mssqlserver_2530"></a>MSSQLSERVER_2530
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
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
 [啟用索引和條件約束](../indexes/enable-indexes-and-constraints.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)  
  
  
