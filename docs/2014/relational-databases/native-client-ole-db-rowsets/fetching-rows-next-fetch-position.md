---
title: 下一個提取位置 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 59af82cea07c73f346c4c8add2cd73e3de2444cc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031002"
---
# <a name="next-fetch-position"></a>下一個提取位置
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會持續追蹤的下一個提取位置因此的一連串的呼叫**GetNextRows**方法 (沒有略過，變更方向，或中介的呼叫**FindNextRow**，**搜尋**，或**的 restartposition 於**方法) 而略過或重複任何資料列不會讀取整個資料列集。 下一個提取位置的變更方式呼叫**irowset:: Getnextrows**， **irowset:: Restartposition**，或**irowsetindex:: Seek**，或藉由呼叫**FindNextRow**具有 null *Findnextrow*值。 呼叫**FindNextRow**包含非 null *Findnextrow*值不會影響下一個提取位置。  
  
## <a name="see-also"></a>另請參閱  
 [擷取資料列](fetching-rows.md)  
  
  