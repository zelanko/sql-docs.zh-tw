---
title: 下一個提取位置 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d6fa0247cafa0d0750f224e3b369965fd4e7989
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423567"
---
# <a name="next-fetch-position"></a>下一個提取位置
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會持續追蹤的下一個提取位置因此，呼叫的序列**GetNextRows**方法 (而略過，不需要變更的方向，或中介呼叫**FindNextRow**， **Seek**，或**restartposition 於**方法) 讀取整個資料列集，而不會略過或重複任何資料列。 下一個提取位置的變更藉由呼叫**irowset:: Getnextrows**， **irowset:: Restartposition**，或**irowsetindex:: Seek**，或藉由呼叫**FindNextRow**具有 null *Findnextrow*值。 呼叫**FindNextRow**使用非 null *Findnextrow*值並不會影響下一個提取位置。  
  
## <a name="see-also"></a>另請參閱  
 [擷取資料列](fetching-rows.md)  
  
  
