---
title: MDSCHEMA_ACTIONS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a68f7e2aa7f12d42c08e7d9226ee5306d0b07021
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemaactions-rowset"></a>MDSCHEMA_ACTIONS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述可用於用戶端應用程式的動作。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_ACTIONS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||資料庫的名稱。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||不支援。 一定會包含**VT_NULL**。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||此動作所屬 Cube 的名稱。|  
|**ACTION_NAME**|**DBTYPE_WSTR**||此動作的名稱。|  
|**ACTION_TYPE**|**DBTYPE_I4**||點陣圖，可用於指定動作的觸發方法。 Msmd.h 檔案為此點陣圖定義下列的位元值常數：<br /><br /> **MDACTION_TYPE_URL** (**0x01**)<br /><br /> **MDACTION_TYPE_HTML** (**0x02**)<br /><br /> **MDACTION_TYPE_STATEMENT** (**0x04**)<br /><br /> **MDACTION_TYPE_DATASET** (**0x08**)<br /><br /> **MDACTION_TYPE_ROWSET** (**0x10**)<br /><br /> **MDACTION_TYPE_COMMANDLINE** (**0x20**)<br /><br /> **MDACTION_TYPE_PROPRIETARY** (**0x40**)<br /><br /> **MDACTION_TYPE_REPORT** (**0x80**)<br /><br /> **MDACTION_TYPE_DRILLTHROUGH** (**0x100**)|  
|**座標**|**DBTYPE_WSTR**||多維度運算式 (MDX) 運算式，指定物件或要在其中執行動作的多維度空間中的座標。 用戶端應用程式必須負責提供此限制資料行的值。<br /><br /> **CORDINATE**必須解析成指定的物件**COORDINATE_TYPE**。|  
|**COORDINATE_TYPE**|**DBTYPE_I4**||點陣圖，指定如何**協調**解譯限制資料行。 Msmd.h 檔案為此點陣圖定義下列的位元值常數：<br /><br /> **MDACTION_COORDINATE_CUBE** (**1**)<br /><br /> **MDACTION_COORDINATE_DIMENSION** (**2**): 參考到維度階層。<br /><br /> **MDACTION_COORDINATE_LEVEL** (**3**)<br /><br /> **MDACTION_COORDINATE_MEMBER** (**4**)<br /><br /> **MDACTION_COORDINATE_SET** (**5**)<br /><br /> **MDACTION_COORDINATE_CELL** (**6**)|  
|**ACTION_CAPTION**|**DBTYPE_WSTR**||如果未指定任何標題，且 DDL 中未指定任何翻譯，則此為動作名稱。<br /><br /> 如果指定了標題或翻譯，以及**CaptionIsMDX**為 false，下列字串的其中之一：<br /><br /> 的適當語言翻譯。<br /><br /> 如果找不到指定之語言的任何轉譯-指定的標題。<br /><br /> 的如果沒有找到翻譯，且 DDL 中未指定標題動作名稱。<br /><br /> 如果指定了標題或翻譯，以及**CaptionIsMDX**為 true，針對指定的語言或指定的轉譯在 DDL 標題中，尋找適當的翻譯和計算所產生的字串若要建立字串的公式。<br /><br /> 如果動作是在 MDX 指令碼中指定，則沒有翻譯，且標題一定會被視為 MDX 運算式。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||動作的易記描述。|  
|**CONTENT**|**DBTYPE_WSTR**||要執行之動作的運算式或內容。|  
|**應用程式**|**DBTYPE_WSTR**||要用於執行動作的應用程式的名稱。|  
|**引動過程**|**DBTYPE_I4**||如何叫用動作的相關資訊：<br /><br /> **MDACTION_INVOCATION_INTERACTIVE** (**1**) 指出在正常作業期間使用的一般動作。 這是此資料行的預設值。<br /><br /> **MDACTION_INVOCATION_ON_OPEN** (**2**) 表示第一次開啟 cube 時，應該執行此動作。<br /><br /> **MDACTION_INVOCATION_BATCH** (**4**) 表示執行的動作是做為批次作業的一部分或[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]工作。<br /><br /> <br /><br /> 請注意中於 Msmd.h 檔案中, 定義這些列舉值。|  
  
 排序資料列集**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **ACTION_NAME**。  
  
> [!NOTE]  
>  動作的**MDACTION_TYPE_PROPRIETARY**型別必須提供值給**應用程式**資料行。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_ACTIONS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性|  
|**CUBE_NAME**|**DBTYPE_WSTR**|強制性|  
|**ACTION_NAME**|**DBTYPE_WSTR**|選擇性|  
|**ACTION_TYPE**|**DBTYPE_I4**|選擇性|  
|**座標**|**DBTYPE_WSTR**|強制性|  
|**COORDINATE_TYPE**|**DBTYPE_I4**|強制性|  
|**引動過程**|**DBTYPE_I4**|（選擇性）**引動過程**限制資料行預設值為**MDACTION_INVOCATION_INTERACTIVE**。 若要擷取的所有動作，請使用**MDACTION_INVOCATION_ALL**值**引動過程**限制資料行。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。 點陣圖，下列有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION (維度)|  
  
> [!IMPORTANT]  
>  **引動過程**限制資料行有預設值是**MDACTION_INVOCATION_INTERACTIVE**。 任何未明確指定此資料行值的結構描述資料列集，都只包含具有此值的資料列。 如果您想要的資料列集包含整個動作集，使用**MDACTION_INVOCATION_ALL**常數中**引動過程**限制資料行。  
  
 用戶端應用程式可以定義一個以上的**ACTION_TYPE**使用 OR 運算子。  
  
## <a name="remarks"></a>備註  
 下表列出有效**協調**和**COORDINATE_TYPE**組合。  
  
|COORDINATE 物件類型|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|**Cube**|**MDACTION_COORDINATE_CUBE**|  
|**維度**|**MDACTION_COORDINATE_DIMENSION**<br /><br /> **MDACTION_COORDINATE_LEVEL**<br /><br /> **MDACTION_COORDINATE_MEMBER**<br /><br /> **MDACTION_COORDINATE_SET**<br /><br /> **MDACTION_COORDINATE_CELL**|  
|**階層架構**|**MDACTION_COORDINATE_DIMENSION**|  
|**Level**|**MDACTION_COORDINATE_LEVEL**|  
|**成員**|**MDACTION_COORDINATE_MEMBER**|  
|**設定**|**MDACTION_COORDINATE_SET**|  
|**資料格**|**MDACTION_COORDINATE_CELL**|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
