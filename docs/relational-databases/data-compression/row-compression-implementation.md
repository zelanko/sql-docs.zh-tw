---
title: 資料列壓縮實作 | Microsoft 文件
ms.custom: ''
ms.date: 06/30/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- compression [SQL Server], row
- row compression [Database Engine]
ms.assetid: dcd97ac1-1c85-4142-9594-9182e62f6832
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2127b9164537afca99b8bd556458137d6713001c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68030521"
---
# <a name="row-compression-implementation"></a>資料列壓縮實作
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  本主題摘要說明 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 如何實作資料列壓縮。 這個摘要提供協助您計畫資料所需之儲存空間的基本資訊。  
  
 啟用壓縮僅會變更與資料類型 (但不與其語法或語意) 相關聯之資料的實體儲存格式。 當啟用一或多個資料表的壓縮時，不需要變更應用程式。 新的記錄儲存格式具有下列的主要變更：  
  
-   降低與記錄相關聯的中繼資料負擔。 此中繼資料是有關資料行、其長度和位移的資訊。 在某些情況下，中繼資料負擔可能會比舊的儲存格式還大。  
  
-   針對數值類型 (例如 **integer**、 **decimal**和 **float**) 以及依據數值的類型 (例如 **datetime** 和 **money**) 使用可變長度儲存格式。  
  
-   使用可變長度格式 (不儲存空白字元) 而儲存固定字元字串。  
  
> [!NOTE]  
>  所有資料類型的 NULL 和 0 值都經過最佳化而不使用任何位元組。  
  
## <a name="how-row-compression-affects-storage"></a>資料列壓縮如何影響儲存  
 下表描述資料列壓縮如何影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]中的現有類型。 此表格不包含可藉由使用頁面壓縮而達成的節省量。  
  
|資料類型|儲存是否受到影響？|描述|  
|---------------|--------------------------|-----------------|  
|**tinyint**|否|所需的最小儲存區是 1 個位元組。|  
|**smallint**|是|如果 1 個位元組能容納此值，只會使用 1 個位元組。|  
|**int**|是|僅使用所需的位元組。 例如，如果值可以儲存在 1 個位元組內，則儲存只會使用 1 個位元組。|  
|**bigint**|是|僅使用所需的位元組。 例如，如果值可以儲存在 1 個位元組內，則儲存只會使用 1 個位元組。|  
|**decimal**|是|此儲存與 Vardecimal 儲存格式完全相同。|  
|**numeric**|是|此儲存與 Vardecimal 儲存格式完全相同。|  
|**bit**|是|中繼資料負荷將此設為 4 個位元。|  
|**smallmoney**|是|藉由使用 4 位元組整數來使用整數資料表示。 貨幣值會乘以 10000，再移除小數點之後的任何數字以儲存產生的整數值。 此類型的儲存最佳化與整數類型類似。|  
|**money**|是|藉由使用 8 位元組整數來使用整數資料表示。 貨幣值會乘以 10000，再移除小數點之後的任何數字以儲存產生的整數值。 此類型的範圍比 **smallmoney**大。 此類型的儲存最佳化與整數類型類似。|  
|**float**|是|將不會儲存最小顯著性位元組為零的項目。 **float** 壓縮主要適用於尾數中的非小數值。|  
|**real**|是|將不會儲存最小顯著性位元組為零的項目。 **real** 壓縮主要適用於尾數中的非小數值。|  
|**smalldatetime**|否|藉由使用兩個 2 位元組整數來使用整數資料表示法。 日期會使用 2 個位元組， 是 1901 年 1 月 1 日之後的日數。 這需要 2 個位元組，從 1902 開始； 因此在該時間點後就無法進行節省。<br /><br /> 時間是午夜之後的分鐘數。 稍微超過 4AM 的時間值會開始使用第二個位元組。<br /><br /> 如果 **smalldatetime** 只會用來表示日期 (常見的情況)，則時間是 0.0。 壓縮會針對資料列壓縮以最大顯著性位元組格式儲存時間而節省 2 個位元組。|  
|**datetime**|是|藉由使用兩個 4 位元組整數來使用整數資料表示。 整數值代表日數，基底日期則是 1900 年 1 月 1 日。 第一個 2 位元組最多可代表到 2079 年。 在該時間點之前，此處的壓縮一定可以節省 2 個位元組。 每個整數值都代表 3.33 毫秒。 壓縮在第一個五分鐘內就會用盡第一個 2 個位元組，而需要在 4PM 之後使用第四個位元組。 因此，在 4PM 之後僅能節省 1 個位元組。 當 **datetime** 像任何其他整數一樣進行壓縮時，壓縮可以在日期中節省 2 個位元組。|  
|**date**|否|藉由使用 3 個位元組來使用整數資料表示法。 這代表從 0001 年 1 月 1 日開始的日期。 對於現代的日期而言，資料列壓縮會使用所有 3 個位元組。 如此不會達成任何節省量。|  
|**time**|否|藉由使用 3 到 6 個位元組來使用整數資料表示法。 有多個以 0 到 9 的有效位數可以使用 3 到 6 個位元組。 壓縮空間的用法如下所示：<br /><br /> **Precision = 0。Bytes = 3**。 每個整數值都代表一秒。 壓縮可藉由使用 2 個位元組而最多代表到 6PM 的時間，因而可能節省 1 個位元組。<br /><br /> **Precision = 1。Bytes = 3**。 每個整數值都代表 1/10 秒。 壓縮在 2AM 之前會使用第三個位元組。 產生的節省量很少。<br /><br /> **Precision = 2。Bytes = 3**。 與前例類似，不太可能達到節省量。<br /><br /> **Precision = 3。Bytes = 4**。 因為在 5AM 之前就會使用了第一個 3 位元組，所以節省的量很少。<br /><br /> **Precision = 4。Bytes = 4**。 在第一個 27 秒內就會使用第一個 3 位元組。 不預期有任何節省量。<br /><br /> **Precision = 5，Bytes = 5** 在中午 12 點之後會使用第五個位元組。<br /><br /> **Precision = 6 和 7，Bytes = 5**。 不會達到任何節省量。<br /><br /> **Precision = 8，Bytes = 6** 在 3AM 之後會使用第六個位元組。<br /><br /> <br /><br /> 請注意，資料列壓縮的儲存沒有變更。 整體而言，無法預期從壓縮 **time** 資料類型達到很大的節省量。|  
|**datetime2**|是|藉由使用 6 到 9 個位元組來使用整數資料表示。 第一個 4 位元組代表日期。 由時間所使用的位元組會依所指定時間的有效位數而定。<br /><br /> 整數值代表自 0001 年 1 月 1 日開始的日數，上限則是 9999 年 12 月 31 日。 為了代表 2005 年中的日期，壓縮會使用 3 個位元組。<br /><br /> 不會節省任何時間，因為它針對不同的時間有效位數而允許 2 到 4 個位元組。 因此，對於一秒鐘的時間有效位數而言，壓縮會為時間使用 2 個位元組，而在 255 秒之後使用第二個位元組。|  
|**datetimeoffset**|是|類似 **datetime2**，但此格式 (HH:MM) 的時區有 2 個位元組。<br /><br /> 與 **datetime2**類似，壓縮可節省 2 個位元組。<br /><br /> 對於時區值，MM 值在多數情況下可能是 0。 因此，壓縮可能可以節省 1 個位元組。<br /><br /> 資料列壓縮的儲存沒有變更。|  
|**char**|是|會移除尾端填補字元。 請注意，不論使用的定序為何， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 都會插入相同的填補字元。|  
|**varchar**|否|沒有影響。|  
|**text**|否|沒有影響。|  
|**nchar**|是|會移除尾端填補字元。 請注意，不論使用的定序為何， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 都會插入相同的填補字元。|  
|**nvarchar**|否|沒有影響。|  
|**ntext**|否|沒有影響。|  
|**binary**|是|會移除尾端的零。|  
|**varbinary**|否|沒有影響。|  
|**image**|否|沒有影響。|  
|**cursor**|否|沒有影響。|  
|**timestamp** / **rowversion**|是|藉由 8 個位元組以使用整數資料表示法。 有針對每個資料庫維護時間戳記計數器，且其值從 0 開始。 這可以像任何其他整數值一般進行壓縮。|  
|**sql_variant**|否|沒有影響。|  
|**uniqueidentifier**|否|沒有影響。|  
|**table**|否|沒有影響。|  
|**xml**|否|沒有影響。|  
|使用者定義型別|否|這在內部表示為 **varbinary**。|  
|FILESTREAM|否|這在內部表示為 **varbinary**。|  
  
## <a name="see-also"></a>另請參閱  
 [資料壓縮](../../relational-databases/data-compression/data-compression.md)   
 [頁面壓縮實作](../../relational-databases/data-compression/page-compression-implementation.md)  
  
  
