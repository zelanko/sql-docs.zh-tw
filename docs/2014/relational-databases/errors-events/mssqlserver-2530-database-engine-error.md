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
manager: craigg
ms.openlocfilehash: 8058c7c31c49935d244726bf9e8ea0ac6cfbe750
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62914569"
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
 [啟用索引和條件約束](../indexes/enable-indexes-and-constraints.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)  
  
  
