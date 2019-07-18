---
title: 在 採礦模型上建立內容查詢 |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98fff978408aa53e030efeceb67af6cc0977597a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210153"
---
# <a name="create-a-content-query-on-a-mining-model"></a>建立採礦模型內容查詢
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  雖然您可以使用 AMO 或 XML/A，以程式設計方式查詢採礦模型內容，但是使用 DMX 來建立查詢是比較簡單的方式。 您也可以針對資料採礦結構描述資料列集建立查詢，方法是建立與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的連接，然後使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]所提供的 DMV 建立查詢。  
  
 下列程序示範如何使用 DMX 來針對採礦模型建立查詢，以及如何查詢資料採礦結構描述資料列集。  
  
 如需如何使用 XML/A 來建立類似查詢的範例，請參閱 [使用 XMLA 建立資料採礦查詢](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md)。  
  
## <a name="querying-data-mining-model-content-by-using-dmx"></a>使用 DMX 來查詢資料採礦模型內容  
  
#### <a name="to-create-a-dmx-model-content-query"></a>建立 DMX 模型內容查詢  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [檢視]  功能表上，按一下 [範本總管]  。  
  
2.  在 [範本總管]  窗格中，按一下 Cube 圖示，即可變更清單並顯示 Analysis Services 範本。  
  
3.  在範本類別目錄的清單中，依序展開 [DMX]  和 [模型內容]  ，然後按兩下 [內容查詢]  。  
  
4.  在 [連接到 Analysis Services]  對話方塊中，選取包含您要查詢之採礦模型的執行個體，然後按一下 [連接]  。  
  
     [內容查詢]  範本就會在適當的程式碼編輯器中開啟。 [中繼資料] 窗格會列出目前資料庫中可用的模型。 若要變更資料庫，請從 [可用的資料庫]  清單中選取不同的資料庫。  
  
5.  在一行中，輸入採礦模型的名稱`FROM`[ *\<採礦模型，name，Mymodel> >* ]`.CONTENT`。 如果採礦模型名稱包含空格，您就必須以方括號括住名稱。  
  
     如果您不想要輸入名稱，可以在 **物件總管** 中選取採礦模型，然後將它拖曳至範本中。  
  
6.  在一行中， `SELECT` *\<選取清單中，運算式清單， \* >* ，輸入採礦模型內容結構描述資料列集中的資料行的名稱。  
  
     若要檢視您可以在採礦模型內容查詢中傳回的資料行清單，請參閱 [採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)所提供的 DMV 建立查詢。  
  
7.  (選擇性) 在範本的 WHERE 子句中輸入條件，以便將傳回的資料列限制為特定節點或值。  
  
8.  按一下 **[執行]** 。  
  
## <a name="querying-the-data-mining-schema-rowsets"></a>查詢資料採礦結構描述資料列集  
  
#### <a name="to-create-a-query-against-the-data-mining-schema-rowset"></a>針對資料採礦結構描述資料列集建立查詢  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [新增查詢]  工具列上，按一下 [Analysis Services DMX 查詢]  或 [Analysis Services MDX 查詢]  。  
  
2.  在 [連接到 Analysis Services]  對話方塊中，選取包含您要查詢之物件的執行個體，然後按一下 [連接]  。  
  
     [內容查詢]  範本就會在適當的程式碼編輯器中開啟。 [中繼資料] 窗格會列出目前資料庫中可用的物件。 若要變更資料庫，請從 [可用的資料庫]  清單中選取不同的資料庫。  
  
3.  在查詢編輯器中，輸入下列項目：  
  
     `SELECT *`  
  
     `FROM $system.DMSCHEMA_MINING_MODEL_CONTENT`  
  
     `WHERE MODEL_NAME = '<model name>'`  
  
4.  按一下 **[執行]** 。  
  
     [結果] 窗格就會顯示模型的內容。  
  
    > [!NOTE]  
    >  若要檢視目前的執行個體上的所有結構描述資料列集，您可以查詢的清單，使用下列查詢：`SELECT * FROM $system.`DISCOVER_SCHEMA_ROWSETS。 或者，如需資料採礦特有之結構描述資料列集的清單，請參閱 [資料採礦結構描述資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets)。  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [資料採礦結構描述資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets)  
  
  
