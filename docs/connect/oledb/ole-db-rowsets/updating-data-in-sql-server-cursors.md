---
title: 更新 SQL Server 資料指標中的資料 | Microsoft Docs
description: 更新 SQL Server 資料指標中的資料
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
ms.openlocfilehash: e5ccf4831cf882eedd4b2b95894d44457402bb6e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994156"
---
# <a name="updating-data-in-sql-server-cursors"></a>更新 SQL Server 資料指標中的資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標擷取和更新資料時，OLE DB Driver for SQL Server 取用者應用程式會由套用到其他任何用戶端應用程式的相同考量和條件約束所繫結。  
  
 只有在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標中的資料列會參與並行的資料存取控制。 取用者要求可修改的資料列集時，並行控制會由 DBPROP_LOCKMODE 所控制。 若要修改並行存取控制的層級，取用者會先設定 DBPROP_LOCKMODE 屬性，然後再開啟資料列集。  
  
 如果用戶端應用程式設計讓交易長時間保持開啟狀態，交易隔離等級可能會對資料列定位造成重大落後。 根據預設，OLE DB Driver for SQL Server 會使用 DBPROPVAL_TI_READCOMMITTED 所指定的讀取認可隔離等級。 當資料列集並行為唯讀時，OLE DB Driver for SQL Server 支援中途讀取隔離。 因此，取用者可以在可修改的資料列集中要求較高的隔離等級，但是無法成功要求任何較低的等級。  
  
## <a name="immediate-and-delayed-update-modes"></a>立即和延遲更新模式  
 在立即更新模式下，**IRowsetChange::SetData** 的每個呼叫會造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的往返。 如果取用者對單一資料列進行多個變更，利用單一 **SetData** 呼叫提交所有變更會更有效率。  
  
 在延遲更新模式下，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的往返是針對 **IRowsetUpdate::Update** 之 *cRows* 和 *rghRows* 參數中指示的每個資料列進行。  
  
 在任一種模式下，當資料列集沒有開啟任何交易物件時，往返代表不同的交易。  
  
 當您使用 **IRowsetUpdate::Update** 時，OLE DB Driver for SQL Server 會嘗試處理每個指示的資料列。 因為任何資料列的資料、長度或狀態值無效所產生的錯誤不會停止 OLE DB Driver for SQL Server 處理。 參與更新的其他所有資料列或沒有任何資料列可能會遭到修改。 當 OLE DB Driver for SQL Server 傳回 DB_S_ERRORSOCCURRED 時，取用者必須檢查傳回的 *prgRowStatus* 陣列來判斷是否有任何特定的資料列發生錯誤。  
  
 取用者不應該假設資料列會以任何特定順序處理。 如果取用者需要透過一個以上的單一資料列進行資料修改的排序處理，取用者應該以應用程式邏輯建立該順序，並開啟交易來包含程序。  
  
## <a name="see-also"></a>另請參閱  
 [更新資料列集中的資料](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
