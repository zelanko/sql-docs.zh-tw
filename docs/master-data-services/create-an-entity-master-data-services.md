---
title: "建立實體 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
caps.latest.revision: 9
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 9b081ac7c85401a43533863f2495dad9032c7ba0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="create-an-entity-master-data-services"></a>建立實體 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，建立實體以包含成員及其屬性。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   模型必須存在。 如需詳細資訊，請參閱[建立模型 &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)。  
  
### <a name="to-create-an-entity"></a>若要建立實體  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [管理模型] 頁面上，從方格中選取您想要為其建立實體的模型，然後按一下 [實體]。  
  
3.  在 [管理實體] 頁面上，按一下 [加入]。  
  
4.  在 [名稱] 方塊中，輸入實體的名稱。  
  
5.  (選擇性) 在 [描述] 欄位中，輸入實體的描述。  
  
6.  或者在 [暫存資料表的名稱] 方塊中，輸入暫存資料表的名稱。  
  
     如果未填寫這個欄位，則會使用實體名稱。  
  
    > [!TIP]  
    >  使用模型名稱當做暫存資料表名稱的一部分，例如 *Modelname_Entityname*。 這樣會更容易在資料庫中找到資料表。 如需暫存資料表的詳細資訊，請參閱[概觀︰從資料表匯入資料 &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)。  
  
7.  在 [交易記錄類型] 欄位中，選擇下拉式清單中的交易記錄類型。  
  
     如需詳細資訊，請參閱[變更實體交易記錄類型 &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
8.  選擇性。 選取 **[自動建立字碼值]** 核取方塊。 如需詳細資訊，請參閱[自動建立代碼 &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)。  
  
9. 選擇性。 選取 [啟用資料壓縮] 核取方塊。 依預設會開啟資料列壓縮。 如需詳細資訊，請參閱 [資料壓縮](../relational-databases/data-compression/data-compression.md)。  
  
10. 按一下 **[儲存]**。  
  
## <a name="grid-columns"></a>方格資料行  
 對於每個建立的實體，會將含有十三個資料行的資料列加入格線。 以下是資料行。  
  
|名稱|說明|  
|----------|-----------------|  
|狀態|實體狀態。 當您按一下 [儲存] 時，下列影像隨即顯示，指出正在更新實體。<br /><br /> ![正在更新狀態圖示](../master-data-services/media/mds-statusicon-updating.png "正在更新狀態圖示")<br /><br /> 如果建立或編輯實體時發生錯誤，則會顯示下列影像。<br /><br /> ![錯誤狀態圖示](../master-data-services/media/mds-statusicon-error.png "錯誤狀態圖示")<br /><br /> 如果狀態正常，則會顯示下列影像。<br /><br /> ![正常狀態圖示](../master-data-services/media/mds-statusicon-ok.png "正常狀態圖示")|  
|名稱|實體名稱。|  
|說明|實體描述。|  
|暫存資料表|此資料表的前置名稱用於儲存資料。|  
|交易記錄類型|實體的交易記錄類型。|  
|自動建立代碼|指定是否啟用自動建立程式碼。|  
|資料壓縮|指定是否啟用實體的資料壓縮。|  
|為同步目標|指定實體是否為同步關聯性的目標。|  
|為已啟用階層|指定是否已啟用實體的明確階層。 若已為實體建立至少一個明確階層，此資料行會顯示 [是]。|  
|建立者|使用者名稱，該使用者建立了實體。|  
|建立於|實體的建立日期和時間。|  
|更新者|使用者名稱，該使用者為最近一次更新模型的使用者。|  
|更新於|實體的上次更新日期與時間。|  
  
## <a name="next-steps"></a>後續步驟  
  
-   [建立文字屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [建立網域屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [建立檔案屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [實體 &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)   
 [明確階層 &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [編輯實體 &#40;Master Data Services&#41;](../master-data-services/edit-an-entity-master-data-services.md)   
 [刪除實體 &#40;Master Data Services&#41;](../master-data-services/delete-an-entity-master-data-services.md)  
  
  

