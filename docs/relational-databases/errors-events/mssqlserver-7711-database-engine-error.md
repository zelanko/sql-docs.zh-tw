---
title: MSSQLSERVER_7711 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7711 (Database Engine error)
ms.assetid: a5c7cd6e-18d6-47ef-902b-db9dd64bba34
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f75bef86a606da4f7103c3afd6c5846dc58e8e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7711"></a>MSSQLSERVER_7711
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|7711|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PRT_RANGE_OVERLAP|  
|訊息文字|資料表或索引或是它的其中一個資料分割已指定 DATA_COMPRESSION 選項一次以上。|  
  
## <a name="explanation"></a>說明  
下列其中一個陳述式中的 DATA_COMPRESSION 選項發生錯誤：  
  
-   CREATE TABLE  
  
-   ALTER TABLE  
  
-   CREATE INDEX  
  
-   ALTER INDEX  
  
如果分割了引用的資料表或索引，則表示其中至少一個分割區已列出 DATA_COMPRESSION 選項一次以上。 如果此資料表或索引未分割，則表示 DATA_COMPRESSION 選項已經引用一次以上。  
  
## <a name="user-action"></a>使用者動作  
如果是已分割的資料表或索引，請確定每一個分割區只指定 DATA_COMPRESSION 選項一次。 如果是未分割的資料表或索引，只能在陳述式中使用 DATA_COMPRESSION 選項一次。  
  
