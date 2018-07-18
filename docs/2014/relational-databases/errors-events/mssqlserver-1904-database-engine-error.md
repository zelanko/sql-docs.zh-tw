---
title: MSSQLSERVER_1904 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 1904 (Database Engine error)
ms.assetid: 2a35d57d-74e2-45a2-8f67-3f2e51d69712
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cbf9281bf87ed9b59c19fcc199e5bdc158857c17
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419527"
---
# <a name="mssqlserver1904"></a>MSSQLSERVER_1904
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|1904|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|KEYCOUNT|  
|訊息文字|資料表 '%.\*ls' 上的 %S_MSG '%.*ls'，其在 %S_MSG 索引鍵清單中有 %d 個資料行名稱。 索引或統計資料索引鍵資料行清單的上限為 %d。|  
  
## <a name="explanation"></a>說明  
 指定之索引或統計資料的索引鍵資料行清單超過允許的資料行數目上限。  
  
## <a name="user-action"></a>使用者動作  
 將索引鍵資料行清單修改成包含不超過指定的資料行數目上限。  
  
 若為非叢集索引，請考慮在 CREATE INDEX 陳述式中使用 INCLUDE 子句，以便將資料行加入至索引，當做非索引鍵資料行。 這個方法可避免超過目前索引大小限制：16 個索引鍵資料行的上限。 如需詳細資訊，請參閱 [建立內含資料行的索引](../indexes/create-indexes-with-included-columns.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [CREATE STATISTICS &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)  
  
  
