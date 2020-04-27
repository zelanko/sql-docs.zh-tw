---
title: 編輯現有的資料來源連接（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.selexistconn.f1
ms.assetid: 97e63f18-a01d-4c91-a411-e7e6d40a0647
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ffc45b255ef609d486f19cf18254ad9ed2937433
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081445"
---
# <a name="edit-an-existing-data-source-connection-ssas-tabular"></a>編輯現有的資料來源連接 (SSAS 表格式)
  本主題描述如何編輯表格式模型中現有資料來源連接的屬性。  
  
 當您建立與外部資料來源的連接之後，就可以依照下列方法來修改該連接：  
  
-   您可以變更連接資訊，包括當做來源使用的檔案、摘要或資料庫、連接的屬性，或是其他提供者特有的連接選項。  
  
-   您可以變更資料表和資料行對應，並移除已不再使用的資料行參考。  
  
-   您可以變更從外部資料來源取得的資料表、檢視表或資料行。  
  
## <a name="modify-a-connection"></a>修改連接  
 此程序描述如何修改資料庫資料來源連接。 使用資料來源的某些選項會因資料來源類型而異，但是您應該能夠輕鬆識別這些差異。  
  
#### <a name="to-change-the-external-data-source-used-by-a-current-connection"></a>若要變更目前連接所使用的外部資料來源  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，按一下 **[模型]** 功能表，然後再按一下 **[現有連接]**。  
  
2.  選取您要修改的資料來源連接，然後按一下 **[編輯]**。  
  
3.  在 **[編輯連接]** 對話方塊中，按一下 **[瀏覽]** ，找出另一個類型相同，但名稱或位置不同的資料庫。  
  
     您一變更資料庫檔案之後，就會出現一則訊息，指出您需要儲存及重新整理資料表，才能看到新的資料。  
  
4.  按一下 **[儲存]**，然後按一下 **[關閉]**。  
  
5.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，依序按一下 **[模型]**、 **[處理]** 及 **[處理全部]**。  
  
     資料表隨即以新的資料來源重新處理，但是會採用原始資料選擇。  
  
    > [!NOTE]  
    >  如果新的資料來源包含了原本不在原始資料來源中的其他任何資料表，您必須重新開啟已變更的連接並加入資料表。  
  
## <a name="edit-table-and-column-mappings-bindings"></a>編輯資料表和資料行對應 (繫結)  
 本程序描述如何在變更資料來源之後編輯對應。  
  
#### <a name="to-edit-column-mappings-when-a-data-source-changes"></a>在資料來源變更時編輯資料行對應  
  
1.  在模型設計師中，選取一個資料表。  
  
2.  按一下 **[資料表]** 功能表，然後再按一下 **[資料表屬性]**。  
  
     所選資料表的名稱會顯示在 **[資料表名稱]** 方塊中。 **[來源名稱]** 方塊會包含此資料表在外部資料來源的名稱。 如果資料行在來源和模型中的名稱不同，您可以在兩組資料行名稱之間切換，其方式是選取 **[來源]** 或 **[模型]** 選項。  
  
3.  若要變更當做資料來源使用的資料表，請針對 **[來源名稱]** 選取與目前資料表不同的資料表。  
  
4.  視需要變更資料行對應：  
  
    1.  若要加入在來源中但是不在模型中的資料行，請選取資料行名稱旁邊的核取方塊。  
  
         下一次當您重新整理時，實際的資料將會載入模型。  
  
    2.  如果目前的資料來源不再提供模型中的某些資料行，通知區域會出現一則訊息，列出無效的資料行。 您不需要進行其他任何處理。  
  
5.  按一下 **[儲存]** ，將變更套用到模型。  
  
     當您儲存目前的資料表屬性集時，可能會出現一則訊息，指出您需要處理資料表。 按一下 **[處理]** ，將更新的資料載入模型中。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS 表格式&#41;處理資料](process-data-ssas-tabular.md)   
 [支援的資料來源 &#40;SSAS 表格式&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
