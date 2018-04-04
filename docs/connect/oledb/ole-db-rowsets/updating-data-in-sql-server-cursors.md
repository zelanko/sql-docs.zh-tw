---
title: 更新 SQL Server 資料指標中的資料 |Microsoft 文件
description: 更新 SQL Server 資料指標中的資料
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2cfc40d1577b1963bfc21aacd0d445275aee80e0
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2018
---
# <a name="updating-data-in-sql-server-cursors"></a>更新 SQL Server 資料指標中的資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  當擷取和更新資料透過[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料指標，取用者應用程式受限於相同考量和條件約束套用至任何其他用戶端應用程式的 SQL Server OLE DB 驅動程式。  
  
 只有在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標中的資料列會參與並行的資料存取控制。 取用者要求可修改的資料列集時，並行控制會由 DBPROP_LOCKMODE 所控制。 若要修改並行存取控制的層級，取用者會先設定 DBPROP_LOCKMODE 屬性，然後再開啟資料列集。  
  
 如果用戶端應用程式設計讓交易長時間保持開啟狀態，交易隔離等級可能會對資料列定位造成重大落後。 根據預設，SQL Server OLE DB 驅動程式會使用 DBPROPVAL_TI_READCOMMITTED 所指定的讀取認可隔離等級。 資料列集並行唯讀時，SQL Server OLE DB 驅動程式支援中途讀取的隔離。 因此，取用者可以在可修改的資料列集中要求較高的隔離等級，但是無法成功要求任何較低的等級。  
  
## <a name="immediate-and-delayed-update-modes"></a>立即和延遲更新模式  
 在立即更新模式中，每個呼叫**irowsetchange:: Setdata**導致往返[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 如果取用者對單一資料列進行多項變更，則更有效率的方式將與單一的所有變更都提交**SetData**呼叫。  
  
 在延遲的更新模式中，對進行往返[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的每個資料列所示*cRows*和*Crows*參數**irowsetupdate:: Update**。  
  
 在任一種模式下，當資料列集沒有開啟任何交易物件時，往返代表不同的交易。  
  
 當您使用**irowsetupdate:: Update**，SQL Server OLE DB 驅動程式會嘗試處理每個指示的資料列。 因為無效的資料、 長度或狀態值值的任何資料列所產生的錯誤不會停止 SQL Server 處理 OLE DB 驅動程式。 參與更新的其他所有資料列或沒有任何資料列可能會遭到修改。 取用者必須檢查傳回*prgRowStatus*陣列來判斷失敗的任何特定的資料列，當 SQL Server OLE DB 驅動程式會傳回 DB_S_ERRORSOCCURRED。  
  
 取用者不應該假設資料列會以任何特定順序處理。 如果取用者需要透過一個以上的單一資料列進行資料修改的排序處理，取用者應該以應用程式邏輯建立該順序，並開啟交易來包含程序。  
  
## <a name="see-also"></a>另請參閱  
 [更新資料集中的資料列集](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
