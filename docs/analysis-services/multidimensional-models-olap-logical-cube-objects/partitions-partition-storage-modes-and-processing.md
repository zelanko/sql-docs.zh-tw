---
title: 資料分割儲存模式及處理 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57c73e3ae9661058277a377b7d17b6a4af393ba0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62640457"
---
# <a name="partitions---partition-storage-modes-and-processing"></a>資料分割 - 資料分割儲存模式及處理
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  資料分割的儲存模式會影響查詢及處理效能、儲存需求，以及此資料分割的儲存位置及其父量值群組和 Cube。 儲存模式的選擇也會影響處理選擇。  
  
 資料分割可以使用三種基本儲存模式之一：  
  
-   多維度 OLAP (MOLAP)  
  
-   關聯式 OLAP (ROLAP)  
  
-   混合式 OLAP (HOLAP)  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援所有的三種基本儲存模式。 另外也支援主動式快取，可以讓您結合 ROLAP 和 MOLAP 儲存的特性，提供資料的立即性和查詢效能。 如需詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
## <a name="molap"></a>MOLAP  
 MOLAP 儲存模式會產生資料分割的彙總，並在處理此資料分割時，將其來源資料的副本儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的多維度結構中； 這個 MOLAP 結構會高度最佳化，以發揮最大的查詢效能。 儲存位置可以在定義資料分割的電腦上，或是在執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的另一部電腦上。 由於來源資料的副本會位於多維度結構中，所以可以在不存取資料分割之來源資料的情況下解析查詢； 查詢回應時間會因為使用彙總而大幅縮減。 此資料分割之 MOLAP 結構中的資料只會維持在與此資料分割的最新處理一樣的最新狀態。  
  
 隨著來源資料的變更，必須要定期處理 MOLAP 儲存中的物件，以便納入這些變更，並將這些變更提供給使用者。 處理時會更新 MOLAP 結構中的資料 (完整更新或累加更新)。 某一個處理和下一個處理之間的時間，會產生一段延遲期間，在這段期間內，OLAP 物件中的資料可能會與來源資料不相符。 您可以用累加或完整方式來更新 MOLAP 儲存中的物件，而不用讓資料分割或 Cube 離線工作； 但是在一些情況下，您可能需要讓 Cube 離線工作，才能夠處理對 OLAP 物件的某些結構性變更。 您可以在臨時伺服器上更新和處理 Cube，並使用資料庫同步處理，將處理好的物件複製到實際伺服器，以減少更新 MOLAP 儲存所需的停機時間。 您也可以使用主動式快取，來減少延遲並提高可用性，同時還保持 MOLAP 儲存的大部分效能優點。 如需詳細資訊，請參閱 <<c0> [ 主動式快取&#40;資料分割&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)，[同步處理 Analysis Services 資料庫](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)，和[處理多維度模型中&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。</c0>  
  
## <a name="rolap"></a>ROLAP  
 ROLAP 儲存模式會將資料分割的彙總儲存在關聯式資料庫內的索引檢視中 (這個關聯式資料庫是指定於資料分割的資料來源中)。 與 MOLAP 儲存模式不同，ROLAP 並不會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料夾中儲存來源資料的副本。 而是在無法從查詢快取中衍生結果時，存取資料來源中的索引檢視來回答查詢。 使用 ROLAP 儲存模式的查詢回應通常會比使用 MOLAP 或 HOLAP 儲存模式的查詢回應慢。 使用 ROLAP 的處理時間通常也比較慢。 但是，ROLAP 會讓使用者即時檢視資料，而且當您在使用不常被查詢的大型資料集 (例如，純綷的記錄資料) 時，可以節省儲存空間。  
  
> [!NOTE]  
>  使用 ROLAP 時，如果合併使用聯結與 GROUP BY 子句，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可能會傳回與未知成員相關的不正確資訊。 而 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會消除關聯式完整性錯誤，而非傳回未知的成員值。  
  
 如果資料分割使用 ROLAP 儲存模式，而其來源資料儲存在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 中，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會嘗試建立索引檢視，以包含資料分割的彙總。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 無法建立索引檢視，則不會建立彙總資料表。 雖然 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會處理在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 上建立索引檢視的工作階段需求，但是 ROLAP 資料分割及其結構描述中的資料表必須符合下列條件，才能讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立彙總的索引檢視：  
  
-   資料分割不能包含使用的量值**最小**或是**Max**彙總函式。  
  
-   ROLAP 資料分割之結構描述中的每份資料表都只能使用一次。 例如，結構描述不能包含 [dbo].[address] AS "Customer Address" 和 [dbo].[address] AS "SalesRep Address"。  
  
-   每個資料表都必須是一個資料表，而不是一個檢視。  
  
-   資料分割之結構描述中的所有資料表名稱都必須具有擁有者的完整名稱 (例如，[dbo].[customer])。  
  
-   資料分割之結構描述中的所有資料表都必須具有相同的擁有者；例如，您不可擁有參考 [tk].[customer]、[john].[store] 和 [dave].[sales_fact_2004] 資料表的 FROM 子句。  
  
-   資料分割之量值的來源資料行不可為 Null。  
  
-   用於檢視中的所有資料表，必須在下列選項設定成 ON 的情況下建立：  
  
    -   ANSI_NULLS  
  
    -   QUOTED_IDENTIFIER  
  
-   在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 中，索引鍵的大小總計不可能超過 900 個位元組。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會判斷提示這個狀況時處理 CREATE INDEX 陳述式，根據固定的長度索引鍵資料行。 不過，如果在索引鍵中有可變長度資料行[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]也會判斷提示這個狀況的基底資料表的每個更新。 因為不同彙總有不同的檢視定義，所以會依彙總設計而定，使用索引檢視的 ROLAP 處理可能成功也可能失敗。  
  
-   建立索引檢視表的工作階段必須有下列選項設為 ON:ARITHABORT、 CONCAT_NULL_YEILDS_NULL、 QUOTED_IDENTIFIER、 ANSI_NULLS、 ANSI_PADDING 和 ANSI_WARNING。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中變更這項設定。  
  
-   建立索引檢視表的工作階段必須有下列選項設為 OFF:NUMERIC_ROUNDABORT。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中變更這項設定。  
  
## <a name="holap"></a>HOLAP  
 HOLAP 儲存模式會結合 MOLAP 和 ROLAP 的屬性。 與 MOLAP 一樣，holap 也會儲存在多維度結構中的資料分割的彙總[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體。 HOLAP 不會儲存來源資料的副本。 針對只存取資料分割彙總之摘要資料的查詢，HOLAP 相當於 MOLAP。 存取來源資料的查詢-例如，如果您想要向下鑽研至不可部分完成的 cube 資料格包括不沒有彙總的資料必須請從關聯式資料庫中擷取資料，並不會以最快速度如果來源資料儲存在 MOLAP structur，其方式是e。 在 HOLAP 儲存模式下，使用者經常會遇到查詢時間有大幅差異的情況，而這是根據可以從快取或彙總來解析查詢，還是從來源資料本身解析查詢而定。  
  
 因為儲存為 HOLAP 的資料分割不包含來源資料，所以會比同等的 MOLAP 資料分割還小，而且針對涉及摘要資料之查詢的回應速度也會比 ROLAP 資料分割還快。 HOLAP 儲存模式一般是適用於 Cube 中的資料分割，而這類資料分割需要根據大量來源資料以快速回應摘要查詢。 但是，如果使用者產生必須接觸分葉層級資料的查詢 (例如計算中間值)，MOLAP 通常是較好的選擇。  
  
## <a name="see-also"></a>另請參閱  
 [主動式快取&#40;資料分割&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [同步處理 Analysis Services 資料庫](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [資料分割 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
