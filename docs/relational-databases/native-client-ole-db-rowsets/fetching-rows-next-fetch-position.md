---
title: 下一個提取位置 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6df5d3e025b16b58f105093ef64278d49f6daa78
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35694819"
---
# <a name="fetching-rows---next-fetch-position"></a>提取資料列的下一個提取位置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會持續追蹤的下一個提取位置因此的一連串的呼叫**GetNextRows**方法 (沒有略過，變更方向，或中介的呼叫**FindNextRow**，**搜尋**，或**的 restartposition 於**方法) 而略過或重複任何資料列不會讀取整個資料列集。 下一個提取位置的變更方式呼叫**irowset:: Getnextrows**， **irowset:: Restartposition**，或**irowsetindex:: Seek**，或藉由呼叫**FindNextRow**具有 null *Findnextrow*值。 呼叫**FindNextRow**包含非 null *Findnextrow*值不會影響下一個提取位置。  
  
## <a name="see-also"></a>另請參閱  
 [擷取資料列](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
  
