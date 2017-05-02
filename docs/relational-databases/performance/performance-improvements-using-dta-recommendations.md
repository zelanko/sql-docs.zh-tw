---
title: "使用 DTA 建議的效能改善 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Engine Tuning Advisor, performance improvements
ms.assetid: 2e51ea06-81cb-4454-b111-da02808468e6
caps.latest.revision: 3
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7722ff42ebc2e4e4515a3097a6b8d1106f5e1287
ms.lasthandoff: 04/11/2017

---
# <a name="performance-improvements-using-dta-recommendations"></a>使用 DTA 建議的效能改善
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]


---
資料倉儲和分析工作負載的效能可大幅獲益於「資料行存放區」****索引，特別是針對需要掃描大型資料表的查詢。 如果查詢存取相對少量的資料來搜尋特定值或某範圍值，則「資料列存放區」**** (B+-樹狀結構) 索引最具效率。 因為資料列存放區索引可依排序順序傳遞資料列，所以也可以減少查詢執行計畫中的排序成本。 因此，資料列存放區與資料行存放區索引組合的建置選擇，是取決於應用程式工作負載。

Database Engine Tuning Advisor (DTA) 是在 SQL Server 2016 中引進，透過分析給定的資料庫工作負載，來建議適合的**資料列存放區與資料行存放區索引組合**。 

為了示範 DTA 工作負載效能建議的優點，我們實驗數個真實的客戶工作負載。 我們讓 DTA 針對每個客戶工作負載分析個別查詢，以及查詢的完整工作負載。 我們考慮三種替代方案︰
  
  1. **僅限資料行存放區**：在不使用 DTA 的情況下，僅建置所有資料表的資料行存放區索引。 
  2. **DTA (僅限資料列存放區)**：搭配執行 DTA 與僅建議資料列存放區索引的選項。
  3. **DTA (資料列存放區 + 資料行存放區)**：搭配執行 DTA 與同時建議資料列存放區和資料行存放區索引的選項。  
   
在每個案例中，我們都會接著實作建議的索引。 我們會報告多次執行查詢或工作負載所取得的平均 CPU 時間 (以毫秒為單位)。 下圖繪製跨兩個不同客戶資料庫之工作負載的 CPU 時間 (以毫秒為單位)。 請注意，y 軸 (CPU 時間) 會使用對數刻度。   


![DTA-columnstore-rowstore-performance](../../relational-databases/performance/media/dta-columnstore-rowstore-performance.gif)



**需要混合實體設計**：第一組長條對應到「客戶 1 第 1 季」。 DTA (資料列存放區 + 資料行存放區) 會建議四個資料行存放區和六個資料列存放區索引的組合，而與僅限資料行存放區索引和 DTA (僅限資料列存放區) 相較之下，這會產生 2.5X – 4X 較少的 CPU 時間。 此示範包含資料列存放區和資料行存放區索引之混合實體設計的優點，*甚至是針對單一查詢*。 

**資料列存放區索引建議的有效性**：第二組和第三組長條 (對應到「客戶 1 第 2 季」和「客戶 2 第 1 季」) 代表查詢具有選擇性篩選述詞，可獲益於適合的資料列存放區索引。 針對這兩個查詢，DTA (僅限資料列存放區) 和 DTA (資料列存放區 + 資料行存放區) 只會建議資料列存放區索引。 這些範例也會示範，即使使用建議資料行存放區索引的選項來叫用 DTA，其成本型方式仍然可確保它只有在工作負載實際從中受益時，才會建議資料行存放區索引。

**資料行存放區索引建議的有效性**：第四組長條對應到「客戶 2 第 2 季」，代表查詢會掃描可獲益於資料行存放區索引的大型資料表。 DTA (僅限資料列存放區) 會產生建議，但與存在資料行存放區索引相較之下，它的 CPU 時間會較高。 DTA (資料列存放區 + 資料行存放區) 會建議適合的資料行存放區索引，因此，符合僅限資料行存放區選項的查詢執行效能。

**具有多個查詢之工作負載建議的有效性**：最後一組長條對應到「客戶 2」的完整工作負載，舉例說明 DTA 可以分析工作負載中的多個查詢，以建議一組適合的資料列存放區和資料行存放區索引，來改善整體工作負載的執行成本。 DTA (資料列存放區 + 資料行存放區) 建議四個資料行存放區索引和十個資料列存放區索引，與僅建置資料行存放區索引相較之下，工作負載會有極大的改善，而與 DTA (僅限資料列存放區) 相較之下，則大約會有 4X–5X 的改善。

總而言之，上述範例說明 DTA 可以適當地利用 SQL Server Database Engine 中支援的資料列存放區和資料行存放區索引，並建議可大幅減少工作負載 CPU 時間的適當索引組合。 

<a name="see-also"></a>另請參閱
---
[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)

[Database Engine Tuning Advisor (DTA) 中的資料行存放區索引建議](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)

[資料行存放區索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)

[資料倉儲的資料行存放區索引](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

[CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)

[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)




