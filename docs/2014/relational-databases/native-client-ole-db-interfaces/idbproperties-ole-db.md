---
title: IDBProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: rothja
ms.author: jroth
ms.openlocfilehash: f42ab47de2471fc413e4c6acf0d6c61cb2b6d77c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056188"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
  OLE DB 標準規格允許提供者將 VT_EMPTY 指定給 `DBPROPINFO::vValues`。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當您呼叫 with 來抓取資料列集屬性時，Native Client OLE DB 一律會傳回 VT_EMPTY `IDBProperties::GetPropertyInfo` `DBPROPSET_ROWSETALL` 。  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
