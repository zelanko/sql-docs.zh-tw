---
title: OPENQUERY （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d8e3b85f3d18b25f9dda1ef4f442ec0822257fae
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670029"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;來源資料查詢 &gt; -OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  以對現有資料來源的查詢取代來源資料查詢。 INSERT、SELECT FROM 預測聯結，以及 SELECT FROM 天然預測聯結語句支援**OPENQUERY**。  
  
## <a name="syntax"></a>語法  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>引數  
 *已命名的 datasource*  
 存在於資料庫上的資料來源 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。  
  
 *查詢語法*  
 傳回資料列集的查詢語法。  
  
## <a name="remarks"></a>備註  
 **OPENQUERY**藉由支援資料來源許可權，提供更安全的方式來存取外部資料。 因為連接字串儲存在資料來源中，所以管理員可以使用資料來源的屬性管理資料的存取。 如需有關資料來源的詳細資訊，請參閱[支援的資料來源 &#40;SSAS-多維度&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional)。  
  
 您可以藉由查詢**MDSCHEMA_INPUT_DATASOURCES**架構資料列集，取得伺服器上可用的資料來源清單。 如需使用**MDSCHEMA_INPUT_DATASOURCES**的詳細資訊，請參閱 MDSCHEMA_INPUT_DATASOURCES 資料列[集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset)。  
  
 您也可以使用下列 DMX 查詢，傳回目前 Analysis Services 資料庫中的資料來源清單：  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>範例  
 下列範例會使用已經在資料庫中定義的 MyDS 資料來源 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 來建立與資料庫的連接 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] ，並查詢**vTargetMail** view。  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#60;來源資料查詢&#62;](../dmx/source-data-query.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
