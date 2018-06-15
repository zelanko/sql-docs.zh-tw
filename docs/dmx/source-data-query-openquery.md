---
title: OPENQUERY (DMX) |Microsoft 文件
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f7b4744c3f521ed4c51e461f2b01a748b9b6496
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842471"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;來源資料查詢&gt;-OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  以對現有資料來源的查詢取代來源資料查詢。 INSERT、 SELECT FROM PREDICTION JOIN，和 SELECT FROM NATURAL PREDICTION JOIN 陳述式支援**OPENQUERY**。  
  
## <a name="syntax"></a>語法  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>引數  
 *具名的資料來源*  
 存在於資料來源[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資料庫。  
  
 *查詢語法*  
 傳回資料列集的查詢語法。  
  
## <a name="remarks"></a>備註  
 **OPENQUERY**提供更安全的方式來存取外部資料支援資料來源權限。 因為連接字串儲存在資料來源中，所以管理員可以使用資料來源的屬性管理資料的存取。 如需有關資料來源的詳細資訊，請參閱[支援資料來源&#40;SSAS-多維度&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)。  
  
 您可以取得一份藉由查詢可用的伺服器的資料來源**MDSCHEMA_INPUT_DATASOURCES**結構描述資料列。 如需有關使用**MDSCHEMA_INPUT_DATASOURCES**，請參閱[MDSCHEMA_INPUT_DATASOURCES 資料列集](../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)。  
  
 您也可以使用下列 DMX 查詢，傳回目前 Analysis Services 資料庫中的資料來源清單：  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>範例  
 下列範例會使用已在中定義的 MyDS 資料來源[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]要建立的連接資料庫[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]資料庫和查詢**vTargetMail**檢視。  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#60;來源資料查詢&#62;](../dmx/source-data-query.md)   
 [資料採礦延伸模組&#40;DMX&#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
