---
title: 更新 SQL Server 資料指標中的資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
ms.assetid: 732dafee-f2d5-4aef-aad7-3a8bf3b1e876
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 788055ec21a215a99b2524310452d14ba390088a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300236"
---
# <a name="updating-data-in-sql-server-cursors"></a>更新 SQL Server 資料指標中的資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  通過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游標獲取和更新數據時,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式使用者應用程式受適用於任何其他用戶端應用程式的相同注意事項和約束的約束。  
  
 只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料指標中的資料列會參與並行的資料存取控制。 取用者要求可修改的資料列集時，並行控制會由 DBPROP_LOCKMODE 所控制。 若要修改並行存取控制的層級，取用者會先設定 DBPROP_LOCKMODE 屬性，然後再開啟資料列集。  
  
 如果用戶端應用程式設計讓交易長時間保持開啟狀態，交易隔離等級可能會對資料列定位造成重大落後。 預設情況下,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式使用 DBPROPVAL_TI_READCOMMITTED 指定的讀取提交的隔離等級。 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]行集併發為唯讀時,本機用戶端 OLE 資料庫提供程式支援髒讀隔離。 因此，取用者可以在可修改的資料列集中要求較高的隔離等級，但是無法成功要求任何較低的等級。  
  
## <a name="immediate-and-delayed-update-modes"></a>立即和延遲更新模式  
 在立即更新模式下，**IRowsetChange::SetData** 的每個呼叫會造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的往返。 如果取用者對單一資料列進行多個變更，利用單一 **SetData** 呼叫提交所有變更會更有效率。  
  
 在延遲更新模式下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的往返是針對 **IRowsetUpdate::Update** 之 *cRows* 和 *rghRows* 參數中指示的每個資料列進行。  
  
 在任一種模式下，當資料列集沒有開啟任何交易物件時，往返代表不同的交易。  
  
 當您使用**IRowsetUpdate::更新**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時, 本機用戶端 OLE 資料庫提供程序嘗試處理每個指示的行。 由於任何行的數據、長度或狀態值無效而發生的錯誤不會停止[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式的處理。 參與更新的其他所有資料列或沒有任何資料列可能會遭到修改。 使用者必須檢查返回的*prgRowStatus 陣列*,以[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]確定當 本機用戶端 OLE DB 提供程式返回DB_S_ERRORSOCCURRED時任何特定行的失敗。  
  
 取用者不應該假設資料列會以任何特定順序處理。 如果取用者需要透過一個以上的單一資料列進行資料修改的排序處理，取用者應該以應用程式邏輯建立該順序，並開啟交易來包含程序。  
  
## <a name="see-also"></a>另請參閱  
 [更新列集中的資料](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
