---
title: 估計資料表的大小 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- pages [SQL Server], space
- space [SQL Server], tables
- row size [SQL Server]
- size [SQL Server], tables
- column size [SQL Server]
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- disk space [SQL Server], tables
- space allocation [SQL Server], table size
- designing databases [SQL Server], estimating size
- reserved free rows per page [SQL Server]
- calculating table size
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 49e63511a23b670575f517640bb0b9f0eb06870a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909026"
---
# <a name="estimate-the-size-of-a-table"></a>估計資料表的大小
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  您可以使用下列步驟來估計將資料儲存於資料表中所需的空間量：  
  
1.  遵循 [估計堆積的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md) 或 [估計叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)中的指示，來計算堆積或叢集索引所需的空間。  
  
2.  對於每個非叢集索引，請遵循 [估計非叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)中的指示，來計算其所需的空間。  
  
3.  新增步驟 1 和 2 中計算的值。  

## <a name="see-also"></a>另請參閱  
 [估計資料庫的大小](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [估計堆積的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [估計叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [估計非叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  
