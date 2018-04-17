---
title: 使用 XMLA 建立資料採礦查詢 |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- content queries [DMX]
ms.assetid: 8f6b6008-006c-4792-9bd1-64c30dc3fd41
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fa60ad8ee91839e04c424c5fe2d23723e495bbd4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-data-mining-query-by-using-xmla"></a>使用 XMLA 建立資料採礦查詢
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]您可以建立各種不同的查詢，針對資料採礦物件使用 AMO、 DMX 或 XML/A  
  
 XML 用於 Analysis Services 伺服器與所有用戶端之間的通訊。 因此，雖然一般而言，使用 DMX 建立內容查詢更為容易，但是您可以使用 XML/A 中的 DISCOVER 和 COMMAND 陳述式撰寫查詢，方法是，使用支援 SOAP 通訊協定的用戶端，或在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中建立 XML/A 查詢。  
  
 本主題說明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供的 XML/A 範本，根據目前伺服器上所儲存的採礦模型，建立模型內容查詢。  
  
## <a name="querying-data-mining-schema-rowsets-by-using-xmla"></a>使用 XML/A 查詢資料採礦結構描述資料列集  
  
#### <a name="to-open-an-xmla-template"></a>開啟 XML/A 範本  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [檢視]  功能表上，按一下 [範本總管] 。  
  
2.  按一下 Cube 圖示，即可開啟 Analysis Services 範本的清單。  
  
3.  在範本類別目錄的清單中，依序展開 [XMLA] 和 [結構描述資料列集]，然後按兩下 [探索結構描述資料列集]，以便在適當的程式碼編輯器中開啟範本。  
  
4.  在 [連接到 Analysis Services] 對話方塊中，填妥連接資訊，再按一下 [連接]。 此時會開啟一個新的查詢編輯器視窗，其中含有 [探索結構描述資料列集] 範本。  
  
#### <a name="to-discover-column-names-from-the-mining-model-content-schema-rowset"></a>從 MINING MODEL CONTENT 結構描述資料列集探索資料行名稱  
  
1.  在 [探索結構描述資料列集] 範本開啟時，按一下 [執行]。  
  
     在 [結果] 窗格中會傳回結構描述資料列集的清單，其中包含目前執行個體提供之所有資料列集的資料列集名稱和資料列集資料行。  
  
2.  在**查詢** 窗格中，放置游標之後**\<限制清單 >**按下 ENTER 即可加入新的一行。  
  
3.  將游標置於空白行和型別 **\<SchemaName > DMSCHEMA_MINING_MODEL_CONTENT\</SchemaName >**  
  
     完整的限制區段應顯示如下：  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<SchemaName>DMSCHEMA_MINING_MODEL_CONTENT</SchemaName>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
4.  按一下 **[執行]**。  
  
     [結果] 窗格會顯示指定之結構描述資料列集的資料行名稱清單。  
  
#### <a name="to-create-a-content-query-using-the-mining-model-content-schema-rowset"></a>使用 MINING MODEL CONTENT 結構描述資料列集建立內容查詢  
  
1.  在 [探索結構描述資料列集] 範本中，取代要求類型標籤內的文字來變更要求類型。  
  
     取代這一行：  
  
     `<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>`  
  
     成為下列這行：  
  
     **\<RequestType > DMSCHEMA_MINING_MODEL_CONTENT\</RequestType >**  
  
2.  將新的條件加入到限制清單中，以便將限制清單變更為依名稱指定採礦模型。  
  
3.  在範本中，將游標放在 `<Restriction List>` 後面，然後按 ENTER 即可加入新的一行。  
  
4.  將游標放在空行上，然後輸入 **<MODEL_NAME>My model name</MODEL_NAME>**  
  
     完整的限制區段應顯示如下：  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<MODEL_NAME>My model name</MODEL_NAME>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
5.  按一下 **[執行]**。  
  
     [結果] 窗格會顯示結構描述定義，以及指定之模型的值。  
  
## <a name="see-also"></a>請參閱  
 [採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [資料採礦結構描述資料列集](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
