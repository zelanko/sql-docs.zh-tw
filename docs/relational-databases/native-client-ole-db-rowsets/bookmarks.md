---
title: "書籤 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- SQL Server Native Client OLE DB provider, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
ms.assetid: 7d9076f2-bf9c-452e-b816-70371a0c1644
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 43b0a2b8453c25b73a6bbfa6e9c24b9b1604056c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="bookmarks"></a>書籤
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  書籤可讓取用者快速地返回資料列。 取用者可以利用書籤，根據書籤值隨機存取資料列。 書籤資料行在資料列集中為資料行 0。 取用者會將繫結結構的 dwFlag 欄位值設定為 DBCOLUMNSINFO_ISBOOKMARK，表示該資料行會當做書籤使用。 取用者也會將資料列集屬性 DBPROP_BOOKMARKS 設定為 VARIANT_TRUE。 這可讓資料行 0 出現在資料列集中。 **Irowsetlocate:: Getrowsat**方法再用來提取資料列，開頭為指定的位移，從書籤的資料列。  
  
## <a name="see-also"></a>請參閱  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
