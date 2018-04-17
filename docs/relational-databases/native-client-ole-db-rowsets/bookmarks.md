---
title: 書籤 |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- SQL Server Native Client OLE DB provider, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
ms.assetid: 7d9076f2-bf9c-452e-b816-70371a0c1644
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4e2d096056d8477481c0a06420db4006abb12fad
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="bookmarks"></a>書籤
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  書籤可讓取用者快速地返回資料列。 取用者可以利用書籤，根據書籤值隨機存取資料列。 書籤資料行在資料列集中為資料行 0。 取用者會將繫結結構的 dwFlag 欄位值設定為 DBCOLUMNSINFO_ISBOOKMARK，表示該資料行會當做書籤使用。 取用者也會將資料列集屬性 DBPROP_BOOKMARKS 設定為 VARIANT_TRUE。 這可讓資料行 0 出現在資料列集中。 **Irowsetlocate:: Getrowsat**方法再用來提取資料列，開頭為指定的位移，從書籤的資料列。  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
