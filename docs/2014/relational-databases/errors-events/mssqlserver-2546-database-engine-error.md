---
title: MSSQLSERVER_2546 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 41e4f62a27a3f4a126c9d25b00c03f7f4c31b933
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022882"
---
# <a name="mssqlserver2546"></a>MSSQLSERVER_2546
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|2546|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_INDEX_MARKED_DISABLED|  
|訊息文字|資料表 'OBJECT_NAME' 上的索引 'INDEX_NAME' 已標示為停用。 請重建索引使其上線。|  
  
## <a name="explanation"></a>說明  
 指定的索引已標示為離線或停用。 因此，無法檢查此索引。  
  
## <a name="user-action"></a>使用者動作  
 使用 ALTER INDEX 來重建索引。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [重新組織與重建索引](../indexes/indexes.md)  
  
  
