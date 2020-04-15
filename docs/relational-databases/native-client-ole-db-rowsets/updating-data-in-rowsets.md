---
title: 更新資料列集中的資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3fed7625eb909327688d7777291b28c7a102dbf6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300218"
---
# <a name="updating-data-in-rowsets"></a>更新資料列集中的資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]消費者更新包含該資料的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可 修改行集時,本機用戶端 OLE 資料庫提供程式會更新數據。 當取用者要求 **IRowsetChange** 或 **IRowsetUpdate** 介面的支援時，就會建立可修改的資料列集。  
  
 所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式可[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]修改的列 集都使用游標來支援行集。 資料列集屬性 DBPROP_LOCKMODE 會改變資料指標中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並行控制行為，並且決定可更新資料列集中的資料列集資料列擷取以及資料完整性錯誤產生的行為。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式支援更新之前或之後的行同步。  
  
> [!NOTE]  
>  IRowChange::SetColumns 可用來設定資料列物件的一或多個具名資料行的值。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [更新 SQL Server 資料指標中的資料](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [重新同步處理資料列](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
