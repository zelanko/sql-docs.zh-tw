---
title: 資料分割和 DirectQuery 模式（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5f179ba9-6efb-46ae-90e5-945bbfddb719
author: minewiskan
ms.author: owend
ms.openlocfilehash: d79b78fbec2a7af13e54547baf294857cebd8dfd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939749"
---
# <a name="partitions-and-directquery-mode-ssas-tabular"></a>資料分割和 DirectQuery 模式 (SSAS 表格式)
  本節說明如何在 DirectQuery 模型中使用資料分割。 如需表格式模型中之資料分割的更一般資訊，請參閱 [資料分割 &#40;SSAS 表格式&#41;](partitions-ssas-tabular.md)。  
  
 如需如何變更所使用之資料分割的指示，或查看資料分割的相關資訊，請參閱[&#40;SSAS 表格式&#41;變更 DirectQuery 資料分割](../change-the-directquery-partition-ssas-tabular.md)。  
  
## <a name="using-partitions-in-directquery-mode"></a>在 DirectQuery 模式中使用資料分割  
 您必須針對每一個資料表指定當做 DirectQuery 資料來源使用的單一資料分割。  如果有多個資料分割，當您將模型切換為啟用 DirectQuery 模式時，根據預設，資料表中建立的第一個資料分割會標示為 DirectQuery 資料分割。 可以在稍後透過使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的資料分割管理員來變更此設定。  
  
 為什麼在 DirectQuery 模式下只允許單一資料分割？  
  
 在表格式模型中 (就如同 OLAP 模型一樣)，資料表的資料分割是由 SQL 查詢所定義。 建立資料分割定義的開發人員會負責確保資料分割不會重疊。 Analysis Services 不會檢查記錄是屬於一個資料分割還是多個資料分割。  
  
 快取表格式模型中資料分割有相同的行為。 如果您使用記憶體中的模型，在存取快取時，會對每個資料分割評估 DAX 公式，並且合併結果。 但是當表格式模型使用 DirectQuery 模式時，無法評估多個資料分割、合併結果，以及將其轉換為 SQL 陳述式以傳送到關聯式資料存放區。 這樣做可能會導致無法接受的效能損失，以及在彙總結果時可能發生的不精確性。  
  
 因此，對於在 DirectQuery 模式中回答的查詢，伺服器會使用已標示為主要資料分割的單一資料分割來存取 DirectQuery，稱為「DirectQuery 資料分割」**。  在這個分割區定義中指定的 SQL 查詢，會定義一組完整的資料，用來回答 DirectQuery 模式中的查詢。  
  
 如果您未明確定義資料分割，則引擎只是發出 SQL 查詢至整個關聯式資料來源、執行 DAX 公式規定的任何以集合為基礎的作業，並且傳回查詢結果。  
  
 如果您在資料表中有多個資料分割，並且選取某個資料分割當做 DirectQuery 資料分割，則預設會將所有其他資料分割標示為僅供記憶體中使用。  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>快取模型和 DirectQuery 模型中的資料分割  
 當您設定 DirectQuery 資料分割時，您必須為此資料分割指定處理選項。  
  
 DirectQuery 資料分割有兩個處理選項。 若要設定這個屬性，請在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用 [資料分割管理員]****，然後選取 [處理選項]**** 屬性。 下表列出這個屬性的值，並描述當每個值在連接字串上結合 DirectQueryUsage 屬性使用時的影響：  
  
|**DirectQueryUsage**屬性|[處理選項]**** 屬性|注意|  
|-----------------------------------|------------------------------------|-----------|  
|DirectQuery|永不處理這個資料分割|當模型使用僅限 DirectQuery 時，不需要進行處理。<br /><br /> 在混合模型中，您可以將 DirectQuery 資料分割設定為永遠不會處理。 例如，如果您正在對一個非常大的資料集進行操作，並且不想要將完整結果新增至快取，則可以指定 DirectQuery 資料分割包含資料表中所有其他資料分割結果的聯集，然後永遠不處理聯集。 傳送至關聯式資料來源的查詢不會受到影響，並且對快取資料執行的查詢會合併來自其他資料分割的資料。|  
|搭配使用 InMemory 和 DirectQuery|允許處理資料分割|如果模型使用混合模式，您應該針對記憶體中查詢和 DirectQuery 資料來源的查詢使用相同資料分割。|  
  
## <a name="see-also"></a>另請參閱  
 [資料分割 &#40;SSAS 表格式&#41;](partitions-ssas-tabular.md)  
  
  
