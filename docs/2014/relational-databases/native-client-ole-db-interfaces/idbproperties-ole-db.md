---
title: IDBProperties (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71999899b70c8eab76e26dba22f09884618277d2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413606"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
  OLE DB 標準規格允許提供者將 VT_EMPTY 指定給 `DBPROPINFO::vValues`。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 一律會傳回 VT_EMPTY，當您呼叫`IDBProperties::GetPropertyInfo`與`DBPROPSET_ROWSETALL`來擷取資料列集屬性。  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
