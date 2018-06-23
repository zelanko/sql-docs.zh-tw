---
title: IDBProperties (OLE DB) |Microsoft 文件
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
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3bee573d18bce37685612ab79a715834ca27e5fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037011"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
  OLE DB 標準規格允許提供者將 VT_EMPTY 指定給 `DBPROPINFO::vValues`。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 一定會傳回 VT_EMPTY 當您呼叫`IDBProperties::GetPropertyInfo`與`DBPROPSET_ROWSETALL`來擷取資料列集屬性。  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  