---
title: 更新資料列集中 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, updating data
- SQL Server Native Client OLE DB provider, data updates
- data updates [SQL Server], OLE DB
ms.assetid: 37769b1c-c480-419a-8c54-5cc420bf73db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f68e4f2be641d6c6aeaf8bbbfcc8cad81ab1a39a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62938679"
---
# <a name="updating-data-in-rowsets"></a>更新資料列集中的資料
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時取用者更新包含之資料的可修改資料列集的資料。 當取用者要求 **IRowsetChange** 或 **IRowsetUpdate** 介面的支援時，就會建立可修改的資料列集。  
  
 所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者可修改的資料列集使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料指標來支援資料列集。 資料列集屬性 DBPROP_LOCKMODE 會改變資料指標中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並行控制行為，並且決定可更新資料列集中的資料列集資料列擷取以及資料完整性錯誤產生的行為。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援更新前後的資料列同步處理。  
  
> [!NOTE]  
>  IRowChange::SetColumns 可用來設定資料列物件的一或多個具名資料行的值。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [更新 SQL Server 資料指標中的資料](updating-data-in-sql-server-cursors.md)  
  
-   [重新同步處理資料列](updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](rowsets.md)  
  
  
