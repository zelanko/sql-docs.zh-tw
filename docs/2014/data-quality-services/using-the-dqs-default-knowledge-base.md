---
title: 使用 DQS 預設知識庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bf7645cbe690898fc1bbad58112a2a61a042aeba
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032735"
---
# <a name="using-the-dqs-default-knowledge-base"></a>使用 DQS 預設知識庫
  本主題說明隨著 **(DQS) 一併安裝的預設知識庫**DQS [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 資料。 這是包含下列定義域之預先建立的預設知識庫：  
  
-   **國家/地區**：包含傳統的完整名稱 (該國家/地區所指定的官方名稱) 和簡短名稱 (清單、地圖等所使用的一般名稱)、兩個字母的縮寫、三個字母的縮寫，以及代表每個地點的三位數代碼。  前置值設定為完整的國家名稱。  
  
-   **國家/地區 (前置三個字母)**：包含傳統的完整名稱 (該國家/地區所指定的官方名稱) 和簡短名稱 (清單、地圖等所使用的一般名稱)、兩個字母的縮寫、三個字母的縮寫，以及代表每個地點的三位數代碼。  前置值設定為三個字母的縣市縮寫。  
  
-   **國家/地區 (前置兩個字母)**：包含傳統的完整名稱 (該國家/地區所指定的官方名稱) 和簡短名稱 (清單、地圖等所使用的一般名稱)、兩個字母的縮寫、三個字母的縮寫，以及代表每個地點的三位數代碼。  前置值設定為兩個字母的國家/地區縮寫。  
  
-   **美國 - 郡**：包含美國各郡的清單。  
  
-   **美國 - 姓氏**：在 2000 年人口普查中出現 100 (含) 次以上的姓氏清單。  
  
-   **美國 - 地點**：包含從 2010 年人口普查擷取之 50 州、哥倫比亞特區以及波多黎各的地點清單。  
  
-   **美國 - 州**：包含美國各州的傳統完整 (官方) 名稱及兩個字母的縮寫。 前置值設定為傳統的州名稱。  
  
-   **美國 - 州 (前置兩個字母)**：包含美國各州的傳統完整 (官方) 名稱及兩個字母的縮寫。 前置值設定為兩個字母的州名縮寫。  
  
## <a name="using-the-default-knowledge-base"></a>使用預設知識庫  
 您可以透過下列方式使用預設的 DQS 知識庫 DQS 資料：  
  
-   使用預設知識庫快速啟動並執行清理資料品質專案，而不需要先在 DQS 中建立新的知識庫。  
  
-   在預設知識庫上執行定義域管理、知識探索或比對原則活動。 若要執行這項操作，請在 [ **Data Quality Client Home Screen** ] 中按一下 [[開啟知識庫]](../../2014/data-quality-services/data-quality-client-home-screen.md)，然後選取 **[開啟知識庫]** 畫面中的 **[DQS 資料]** 知識庫，再選取 **[選取活動]** 區域中的必要活動。 按 **[下一步]** 繼續進行。  
  
-   使用預設知識庫建立新的知識庫。 若要從現有的知識庫建立知識庫，請參閱＜ [Create a Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md)＞。  
  
-   在 [Integration Services 中的 DQS 清理元件](http://go.microsoft.com/fwlink/?LinkId=238830) 及 [Excel 的 Master Data Services 增益集](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)中使用。  
  
## <a name="see-also"></a>另請參閱  
 [DQS 知識庫與網域](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
