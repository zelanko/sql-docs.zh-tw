---
title: 索引磁碟空間範例 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- online index disk space
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- offline index disk space [SQL Server]
ms.assetid: e5c71f55-0be3-4c93-97e9-7b3455c8f581
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1d85fecce4c5b97154312922ed96f988754f88e0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85668284"
---
# <a name="index-disk-space-example"></a>索引磁碟空間範例
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  無論何時建立、重建或卸除索引，舊結構 (來源) 和新結構 (目標) 兩者在它們適當的檔案和檔案群組中都需要磁碟空間。 舊結構要到索引建立交易認可時才會取消配置。 此時也可能會需要額外暫存磁碟空間，以供排序作業。 如需詳細資訊，請參閱 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)。  
  
 在此範例中，會決定建立叢集索引的磁碟空間需求。  
  
 假設在建立叢集索引之前，發生下列狀況：  
  
-   現有的資料表 (堆積) 包含 1 百萬個資料列。 每一個資料列的長度為 200 位元組。  
  
-   非叢集索引 A 包含 1 百萬個資料列。 每一個資料列的長度為 50 位元組。  
  
-   非叢集索引 B 包含 1 百萬個資料列。 每一個資料列的長度為 80 位元組。  
  
-   index create memory 選項設定為 2 MB。  
  
-   所有現有的和新的索引採用 80 的填滿因數值。 這表示有 80% 的分頁是滿的。  
  
    > [!NOTE]  
    >  建立叢集索引之後，必須重建兩個非叢集索引以取代有新的叢集索引鍵的資料列指標。  
  
## <a name="disk-space-calculations-for-an-offline-index-operation"></a>離線索引作業的磁碟空間計算  
 下列步驟中，會計算索引作業期間使用的暫存磁碟空間和儲存新索引的永久磁碟空間。 顯示的計算是近似值；結果是四捨五入並且只考慮索引分葉層級的大小。 波浪號 (~) 是用來表示近似的計算。  
  
1.  決定來源結構的大小。  
  
     堆積：1 百萬 * 200 位元組 ~ 200 MB  
  
     非叢集索引 A：1 百萬 * 50 位元組 / 80% ~ 63 MB  
  
     非叢集索引 B：1 百萬 * 80 位元組 / 80% ~ 100 MB  
  
     現有結構的總計大小：363 MB  
  
2.  決定目標索引結構的大小。 假設新的叢集索引鍵的長度是 24 個位元組，包含唯一識別值。 兩個非叢集索引的資料列指標 (長度為 8 個位元組) 會以此叢集索引鍵取代。  
  
     叢集索引：1 百萬 * 200 位元組 / 80% ~ 250 MB  
  
     非叢集索引 A：1 百萬 * (50 - 8 + 24) 位元組 / 80% ~ 83 MB  
  
     非叢集索引 B：1 百萬 * (80 - 8 + 24) 位元組 / 80% ~ 120 MB  
  
     新結構的總計大小：453 MB  
  
     索引作業期間支援來源和目標結構所需的總磁碟空間是 816 MB (363 + 453)。 在索引作業認可之後，將會重新配置目前對來源結構配置的空間。  
  
3.  決定額外的暫存磁碟空間以供排序。  

     會顯示在 **tempdb** 排序 (SORT_IN_TEMPDB 設為 ON) 和在目標位置排序 (SORT_IN_TEMPDB 設為 OFF) 的空間需求。  
  
    1.  當 SORT_IN_TEMPDB 設為 ON 時， **tempdb** 必須有足夠的磁碟空間，才能保留最大的索引 (1 百萬 * 200 位元組 ~ 200 MB)。 在排序作業中不考慮填滿因數。  
  
         額外的磁碟空間 (在 **tempdb** 位置) 等於 [設定 index create memory 伺服器組態選項](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) 值 = 2 MB。  
  
         當 SORT_IN_TEMPDB 設為 ON 時，暫存磁碟空間的總計大小 ~ 202 MB。  
  
    2.  當 SORT_IN_TEMPDB 設為 OFF (預設) 時，步驟 2 中為新索引所考慮的 250 MB 磁碟空間是用來排序。  
  
         額外的磁碟空間 (在目標位置) 等於 [設定 index create memory 伺服器組態選項](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) 值 = 2 MB。  
  
         當 SORT_IN_TEMPDB 設為 OFF 時，暫存磁碟空間的總計大小 = 2 MB。  
  
 使用 **tempdb**，建立叢集和非叢集索引會需要總共 1018 MB (816 + 202) 的大小。 雖然使用 **tempdb** 會增加建立索引所需的暫存磁碟空間數量，但只要 **tempdb** 所在的磁碟集與使用者資料庫不同，就可以減少建立索引所需的時間。 如需使用 **tempdb**的詳細資訊，請參閱 [索引的 SORT_IN_TEMPDB 選項](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)。  
  
 不使用 **tempdb**，建立叢集和非叢集索引會需要總共 818 MB (816+ 2) 的大小。  
  
## <a name="disk-space-calculations-for-an-online-clustered-index-operation"></a>線上叢集索引作業的磁碟空間計算  
 當您在線上建立、卸除或重建叢集索引時，需要額外的磁碟空間才能建立並維護暫存的對應索引。 此暫存對應索引包含資料表中每一個資料列的一筆記錄，並且其內容是舊的和新的書籤資料行的聯集。  
  
 若要計算線上叢集索引作業所需的磁碟空間，請按照離線索引作業的步驟，並且將結果加到下列步驟的結果。  
  
-   決定暫存對應索引的空間。  
  
     在此範例中，舊的書籤是堆積 (8 位元組) 的資料列識別碼 (RID)，而新的書籤是叢集索引鍵 (24 位元組，包括 **唯一識別值**)。 舊書籤和新書籤之間沒有重疊的資料行。  
  
     暫存對應索引大小 = 1 百萬 * (8 位元組 + 24 位元組) / 80% ~ 40 MB。  
  
     如果 SORT_IN_TEMPDB 設為 OFF，此磁碟空間必須加到目標位置中所需的磁碟空間；如果 SORT_IN_TEMPDB 設為 ON，此磁碟空間必須加到 **tempdb** 。  
  
 如需暫存對應索引的詳細資訊，請參閱 [索引 DDL 作業的磁碟空間需求](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)。  
  
## <a name="disk-space-summary"></a>磁碟空間摘要  
 下表摘要出磁碟空間計算的結果。  
  
|索引作業|下列結構中，不同位置的磁碟空間需求|  
|---------------------|---------------------------------------------------------------------------|  
|離線索引作業，SORT_IN_TEMPDB = ON|作業期間的總空間：1018 MB<br /><br /> -現有的資料表和索引：363 MB\*<br /><br /> -<br />                    **tempdb**：202 MB*<br /><br /> -新的索引：453 MB<br /><br /> 作業之後所需的總空間：453 MB|  
|離線索引作業，SORT_IN_TEMPDB = OFF|作業期間的總空間：816 MB<br /><br /> -現有的資料表和索引：363 MB*<br /><br /> -新的索引：453 MB<br /><br /> 作業之後所需的總空間：453 MB|  
|線上索引作業，SORT_IN_TEMPDB = ON|作業期間的總空間：1058 MB<br /><br /> -現有的資料表和索引：363 MB\*<br /><br /> -<br />                    **tempdb** (包含對應索引)：242 MB*<br /><br /> -新的索引：453 MB<br /><br /> 作業之後所需的總空間：453 MB|  
|線上索引作業，SORT_IN_TEMPDB = OFF|作業期間的總空間：856 MB<br /><br /> -現有的資料表和索引：363 MB*<br /><br /> -暫存對應索引：40 MB\*<br /><br /> -新的索引：453 MB<br /><br /> 作業之後所需的總空間：453 MB|  
  
 \* 此空間在索引作業認可之後會重新配置。  
  
 此範例不考慮任何 **tempdb** 中，並行使用者更新及刪除作業建立的版本記錄所需的額外暫存磁碟空間。  
  
## <a name="related-content"></a>相關內容  
 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [索引作業的交易記錄磁碟空間](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)  
  
  
