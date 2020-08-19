---
description: 清理複合定義域中的資料
title: 清理複合定義域中的資料
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d1076e0-7710-469a-9107-e293e4bd80ac
author: swinarko
ms.author: sawinark
ms.openlocfilehash: f35430d590be36bb7ae487d32a9a0fc97c0275ce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449942"
---
# <a name="cleanse-data-in-a-composite-domain"></a>清理複合定義域中的資料

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  本主題會提供有關在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中清理複合定義域的資訊。 複合定義域是由兩個或多個單一定義域所組成，而且會對應至由多個相關詞彙所組成的資料欄位。 複合定義域中的個別定義域必須擁有共同知識領域。 如需有關複合定義域的詳細資訊，請參閱＜ [Managing a Composite Domain](../data-quality-services/managing-a-composite-domain.md)＞。  
  
##  <a name="mapping-a-composite-domain-to-the-source-data"></a><a name="Mapping"></a> 將複合定義域對應至來源資料  
 有兩種方式可將來源資料對應至複合定義域：  
  
-   來源資料是對應至複合定義域的單一欄位 (比方說完整名稱)。  
  
    -   如果複合定義域對應至參考資料服務，來源資料將會以原本樣子傳送給參考資料服務進行更正和剖析。  
  
    -   如果複合定義域未對應至參考資料服務，則會根據為複合定義域定義的剖析方法加以剖析。 如需有關指定複合定義域之剖析方法的詳細資訊，請參閱＜ [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)＞。  
  
-   來源資料是由多個欄位所組成 (比方說名字、中間名和姓氏)，這些欄位會對應至複合定義域內的個別定義域。  
  
 如需如何將複合定義域對應至來源資料的範例，請參閱[將定義域或複合定義域附加至參考資料](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)。  
  
##  <a name="data-correction-using-definitive-cross-domain-rules"></a><a name="CDCorrection"></a> 使用最終跨定義域規則的資料更正  
 複合定義域中的跨定義域規則可讓您建立規則，以指示複合定義域內個別定義域之間的關聯性。 當您針對與複合定義域有關的來源資料執行清理活動時，跨定義域規則會列入考量。 除了只讓您知道跨定義域規則是否有效之外，最終 *Then* 跨定義域規則 **[值等於]** 也會在資料清理活動期間更正資料。  
  
 假設有以下範例：有一個複合定義域 Product 具有三個個別定義域：ProductName、CompanyName 和 ProductVersion。 請建立以下最終跨定義域規則：  
  
 如果定義域 'CompanyName' 值包含 *Microsoft* 而且定義域 ‘ProductName’ 值等於 *Office* 且 'ProductVersion' 值等於 *2010*，則定義域 'ProductName' 值等於 *Microsoft Office 2010*。  
  
 當執行此跨定義域規則時，來源資料 (ProductName) 會在清理活動之後更正為以下項目：  
  
 **來源資料**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Office|Microsoft Inc.|2010|  
  
 **輸出資料**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Microsoft Office 2010|Microsoft Inc.|2010|  
  
 當您測試最終 *Then* 跨定義域規則 **[值等於]** 時， **[測試複合定義域規則]** 對話方塊會包含新的資料行 **[更正為]**，此資料行會顯示正確資料。 在清理資料品質專案中，這個最終跨定義域規則會將資料變更為100% 信賴，而 **Reason** 資料行會顯示下列訊息：由規則 ' ' 更正 *\<Cross-Domain Rule Name>* 。 如需有關跨定義域規則的詳細資訊，請參閱＜ [Create a Cross-Domain Rule](../data-quality-services/create-a-cross-domain-rule.md)＞。  
  
> [!NOTE]  
>  最終跨定義域規則將不適用於附加至參考資料服務的複合定義域。  
  
##  <a name="data-profiling-for-composite-domains"></a><a name="DataProfiling"></a> 複合定義域的資料分析  
 DQS 分析會在清理活動期間提供兩個資料品質維度： *完整性* (資料存在的程度) 和 *精確度* (可將資料用於預定用途的程度)。 分析可能不會針對複合定義域提供可靠的完整性統計資料。 如果您需要完整性統計資料，請使用單一定義域，而非複合定義域。 如果您想要使用複合定義域，您可能會想要使用分析用的單一定義域來建立一個知識庫以判斷完整性，並使用清理活動所用的複合定義域來建立另一個定義域。 例如，分析可能會針對使用複合定義域的位址記錄顯示 95% 完整性，但是其中一個資料行可能會有更高層級的不完整性，例如郵遞區號 (zip) 資料行。 在此範例中，您可能會想要使用單一定義域衡量郵遞區號資料行的完整性。  
  
 分析可能會針對複合定義域提供可靠的精確度統計資料，因為您可以一起衡量多個資料行的精確度。 此資料的值位於複合彙總中，所以您可能會想要使用複合定義域衡量精確度。  
  
 如需清理活動期間的資料分析詳細資訊，請參閱[使用 DQS &#40;內部&#41; 知識清理資料](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)中的[分析工具統計資料](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Profiler)。  
  
  
