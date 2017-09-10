---
title: "DMSCHEMA_MINING_MODEL_CONTENT 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_MODEL_CONTENT
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT rowset
ms.assetid: 1e85d9e7-3b74-42ac-b94e-f52f76d8a25d
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7d48b47cc0ded0541380a4a9997b1cab13bd21a0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingmodelcontent-rowset"></a>DMSCHEMA_MINING_MODEL_CONTENT 資料列集
  允許用戶端應用程式瀏覽資料採礦模型中的內容。 用戶端應用程式可使用本主題結尾處所述的特殊樹狀作業限制，以導覽採礦模型的內容。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_MODEL_CONTENT**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||目錄的名稱。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]擴展此資料行的模型是成員的資料庫名稱。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||不合格的結構描述名稱。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**VT_NULL**。|  
|**MODEL_NAME**|**DBTYPE_WSTR**||與此資料列所述的內容相關聯的模型名稱。|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||對應至這個節點之屬性的名稱。|  
|**NODE_NAME**|**DBTYPE_WSTR**||節點的名稱。 目前，此資料行包含相同的值**NODE_UNIQUE_NAME**，但是這可能會在未來版本中變更。|  
|**NODE_UNIQUE_NAME**|**DBTYPE_WSTR**||節點的唯一名稱。|  
|**NODE_TYPE**|**DBTYPE_I4**||節點類型。 將產生下列其中一個值 (協力廠商資料採礦演算法可以擴充此清單)：<br /><br /> **DM_NODE_TYPE_CLASSIFICATION_TREE_ROOT** (**2**)<br /><br /> **DM_NODE_TYPE_TREE_INTERIOR** (**3**)<br /><br /> **DM_NODE_TYPE_TREE_DISTRIBUTION** (**4**)<br /><br /> **DM_NODE_TYPE_CLUSTER** (**5**)<br /><br /> **DM_NODE_TYPE_UNKNOWN** (**6**)<br /><br /> **DM_NODE_TYPE_ITEMSET** (**7**)<br /><br /> **DM_NODE_TYPE_ASSOCIATION_RULE** (**8**)<br /><br /> **DM_NODE_TYPE_NB_PREDICTABLE_ATTRIBUTE** (**9**)<br /><br /> **DM_NODE_TYPE_NB_INPUT_ATTRIBUTE** (**10**)<br /><br /> **DM_NODE_TYPE_NB_INPUT_ATTRIBUTE_STATE** (**11**)<br /><br /> **DM_NODE_TYPE_SEQUENCE** (**13**)<br /><br /> **DM_NODE_TYPE_TRANSITION** (**14**)<br /><br /> **DM_NODE_TYPE_TIME_SERIES** (**15**)<br /><br /> **DM_NODE_TYPE_TS_TREE** (**16**)<br /><br /> **DM_NODE_TYPE_NN_SUBNETWORK** (**17**) 類神經網路，子網路<br /><br /> **DM_NODE_TYPE_NN_INPUT_LAYER** (**18**) 類神經網路，輸入層 （輸入節點的父系）<br /><br /> **DM_NODE_TYPE_NN_HIDDEN_LAYER** (**19**) 類神經網路，隱藏層 （隱藏節點的父系）<br /><br /> **DM_NODE_TYPE_NN_OUTPUT_LAYER** (**20**) 類神經網路，輸出層 （輸入節點的父系）<br /><br /> **DM_NODE_TYPE_NN_INPUT_NODE** (**21**) 類神經網路，輸入的節點<br /><br /> **DM_NODE_TYPE_NN_HIDDEN_NODE** (**22**) 類神經網路，隱藏的節點<br /><br /> **DM_NODE_TYPE_NN_OUTPUT_NODE** (**23**) 類神經網路，輸出節點<br /><br /> **DM_NODE_TYPE_NN_MARGINAL_STAT_NODE** (**24**) 類神經網路，臨界統計資料節點<br /><br /> **DM_NODE_TYPE_REGRESSION_TREE_ROOT** (**25**)<br /><br /> **DM_NODE_TYPE_NB_MARGINAL_STAT_NODE** (**26**) 類神經網路，臨界統計資料節點|  
|**NODE_GUID**|**DBTYPE_GUID**||節點 GUID。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**NODE_CAPTION**|**DBTYPE_WSTR**||與節點關聯的標籤或標題。 這個屬性主要是供顯示之用。|  
|**CHILDREN_CARDINALITY**|**DBTYPE_UI4**||節點所擁有子系數目的估計。|  
|**PARENT_UNIQUE_NAME**|**DBTYPE_WSTR**||節點之父系的唯一名稱。 **NULL**的任何根層級的節點都會傳回。|  
|**NODE_DESCRIPTION**|**DBTYPE_WSTR**||使用者易記的節點描述。|  
|**NODE_RULE**|**DBTYPE_WSTR**||節點中內嵌之規則的 XML 描述。|  
|**MARGINAL_RULE**|**DBTYPE_WSTR**||從父節點移至節點之規則的 XML 描述。|  
|**NODE_PROBABILITY**|**DBTYPE_R8**||與此節點關聯的機率。|  
|**MARGINAL_PROBABILITY**|**DBTYPE_R8**||從父節點到達節點的機率。|  
|**NODE_DISTRIBUTION**|**DBTYPE_HCHAPTER**||包含節點之機率長條圖的資料表。|  
|**NODE_SUPPORT**|**DBTYPE_R8**||支援這個節點的案例數目。|  
|**MSOLAP_MODEL_COLUMN**|**DBTYPE_WSTR**||來自與此節點相關之模型定義的資料行名稱。|  
|**MSOLAP_NODE_SCORE**|**DBTYPE_R8**||此節點已計算出來的分數。|  
|**MSOLAP_NODE_SHORT_CAPTION**|**DBTYPE_WSTR**||節點的簡短標題，做為顯示之用並可改善可讀性。|  
  
## <a name="restriction-columns"></a>限制資料行  
 **DMSCHEMA_MINING_MODEL_CONTENT**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**NODE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**NODE_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**NODE_TYPE**|**DBTYPE_I4**|選擇性。|  
|**NODE_GUID**|**DBTYPE_WSTR**|選擇性。|  
|**NODE_CAPTION**|**DBTYPE_WSTR**|選擇性。|  
|**TREE_OPERATION**|**DBTYPE_UI4**|選擇性。 請參閱下列其他備註。|  
  
 限制**TREE_OPERATION**，不在任何特定的資料行上**DMSCHEMA_MINING_MODEL_CONTENT**資料列集; 相反地，它會指定樹狀運算子。 取用者可以指定**NODE_UNIQUE_NAME**限制以及樹狀運算子 (**祖系**，**子系**，**同層級**， **父**，**下階**，**自助**) 若要取得之成員的要求的集合。 **自助**運算子傳回的資料列清單中包括節點本身的資料列。 下表描述組成之點陣圖定義的常數**TREE_OPERATION**限制。 也可以結合使用邏輯**或**運算子。  
  
|常數|值|  
|--------------|-----------|  
|**DMTREEOP_ANCESTORS**|**0x00000020**|  
|**DMTREEOP_CHILDREN**|**0x00000001**|  
|**DMTREEOP_SIBLINGS**|**0x00000002**|  
|**DMTREEOP_PARENT**|**0x00000004**|  
|**DMTREEOP_SELF**|**0x00000008**|  
|**DMTREEOP_DESCENDANTS**|**0x00000010**|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
