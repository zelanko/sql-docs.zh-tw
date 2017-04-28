---
title: MSSQLSERVER_10737 | Microsoft Docs
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
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 591b8634e244f472fd5051fde842f4bf9428c4d4
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver10737"></a>MSSQLSERVER_10737
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|MSSQLSERVER|  
|事件識別碼|10737|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|REBUILD_PARTITION_ALL_NOT_SPECIFIED|  
|訊息文字|在 ALTER TABLE REBUILD 或 ALTER INDEX REBUILD 陳述式中，如果在 DATA_COMPRESSION 子句中指定了分割區，就必須指定 PARTITION=ALL。 PARTITION=ALL 子句是用來強調即將重建資料表或索引的所有分割區，即使 DATA_COMPRESSION 子句中只有指定子集也一樣。|  
  
## <a name="user-action"></a>使用者動作  
將 PARTITION=ALL 子句加入至 ALTER TABLE 或 ALTER INDEX 陳述式。 或者，若要重建特定資料分割，請使用 REBUILD PARTITION = \<分割區編號運算式> WITH (DATA_COMPRESSION={ON | OFF})。  
  

