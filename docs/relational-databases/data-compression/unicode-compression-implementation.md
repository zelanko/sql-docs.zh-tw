---
title: Unicode 壓縮實作 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Unicode data compression
- compression [SQL Server], Unicode data
ms.assetid: 44e69e60-9b35-43fe-b9c7-8cf34eaea62a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6017aa60035ab15b80bf596aa06fce20bd141331
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="unicode-compression-implementation"></a>Unicode 壓縮實作
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 Standard Compression Scheme for Unicode (SCSU) 演算法的實作來壓縮儲存在資料列或頁面壓縮物件中的 Unicode 值。 對於這些壓縮的物件而言，系統會自動針對 **nchar(n)** 和 **nvarchar(n)** 資料行進行 Unicode 壓縮。 不論地區設定為何， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 都會將 Unicode 資料儲存成 2 位元組。 這稱為 UCS-2 編碼。 對於某些地區設定而言，SQL Server 中的 SCSU 壓縮實作最多可以節省 50% 的儲存空間。  
  
## <a name="supported-data-types"></a>支援的資料類型  
 Unicode 壓縮支援固定長度的 **nchar(n)** 和 **nvarchar(n)** 資料類型。 不過，無法壓縮以非資料列方式儲存或儲存在 **nvarchar(max)** 資料行中的資料值。  
  
> [!NOTE]  
>  不支援 **nvarchar(max)** 資料使用 Unicode 壓縮，即使此資料儲存於資料列中。 但是，此資料類型仍可以從頁面壓縮中受益。  
  
## <a name="upgrading-from-earlier-versions-of-sql-server"></a>從舊版 SQL Server 升級  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時，系統不會對任何資料庫物件 (已壓縮或未壓縮) 進行與 Unicode 壓縮相關的變更。 升級資料庫之後，受影響的物件如下所示：  
  
-   如果某個物件未壓縮，就不會進行任何變更，而且此物件將繼續如同先前的方式運作。  
  
-   資料列或頁面壓縮的物件將繼續如同先前的方式運作。 未壓縮的資料會維持未壓縮的形式，直到更新其值為止。  
  
-   插入資料列或頁面壓縮資料表的新資料列將使用 Unicode 壓縮進行壓縮。  
  
    > [!NOTE]  
    >  若要充分運用 Unicode 壓縮的優點，您必須使用頁面或資料列壓縮來重建物件。  
  
## <a name="how-unicode-compression-affects-data-storage"></a>Unicode 壓縮如何影響資料儲存  
 如果您建立或重建某個索引，或在使用資料列或頁面壓縮進行壓縮的資料表中變更某個值，只有當受影響之索引或值的壓縮大小小於目前的大小時，系統才會以壓縮方式進行儲存。 這樣做可避免資料表中的資料列或索引由於 Unicode 壓縮而增加大小。  
  
 壓縮所節省的儲存空間主要取決於所壓縮之資料的特性以及資料的地區設定。 下表將列出許多地區設定可達成的空間節省效果。  
  
|地區設定|壓縮百分比|  
|------------|-------------------------|  
|英文|50%|  
|德文|50%|  
|Hindi|50%|  
|土耳其文|48%|  
|越南文|39%|  
|日文|15%|  
  
## <a name="see-also"></a>另請參閱  
 [資料壓縮](../../relational-databases/data-compression/data-compression.md)   
 [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)   
 [頁面壓縮實作](../../relational-databases/data-compression/page-compression-implementation.md)   
 [sys.dm_db_persisted_sku_features &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-persisted-sku-features-transact-sql.md)  
  
  
