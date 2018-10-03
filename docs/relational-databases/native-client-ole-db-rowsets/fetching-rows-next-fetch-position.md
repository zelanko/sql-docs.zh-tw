---
title: 下一個提取位置 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 529580a01fc0ca44aaaa68db7524efc80c985140
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638986"
---
# <a name="fetching-rows---next-fetch-position"></a>擷取資料列 - 下一個擷取位置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會持續追蹤的下一個提取位置因此，呼叫的序列**GetNextRows**方法 (而略過，不需要變更的方向，或中介呼叫**FindNextRow**， **Seek**，或**restartposition 於**方法) 讀取整個資料列集，而不會略過或重複任何資料列。 下一個提取位置的變更方式為：呼叫 **IRowset::GetNextRows**、**IRowset::RestartPosition** 或 **IRowsetIndex::Seek**，或者呼叫包含 Null *pBookmark* 值的 **FindNextRow**。 呼叫包含非 Null *pBookmark* 值的 **FindNextRow** 不會影響下一個提取位置。  
  
## <a name="see-also"></a>另請參閱  
 [擷取資料列](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
  
