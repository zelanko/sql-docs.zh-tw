---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7d89c05ebd0b181b63f66fa0e0e0db99d54b952
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916142"
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
  
  
