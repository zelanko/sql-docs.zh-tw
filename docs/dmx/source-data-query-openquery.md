---
description: '&lt;來源資料查詢 &gt; -OPENQUERY'
title: OPENQUERY (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 62d638b6b6028ffa861460e07f2283cb7380e129
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726102"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;來源資料查詢 &gt; -OPENQUERY
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  以對現有資料來源的查詢取代來源資料查詢。 INSERT、SELECT FROM 預測聯結，以及 SELECT FROM 自然預測聯結語句支援 **OPENQUERY**。  
  
## <a name="syntax"></a>語法  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>引數  
 *命名的 datasource*  
 存在於資料庫上的資料來源 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。  
  
 *查詢語法*  
 傳回資料列集的查詢語法。  
  
## <a name="remarks"></a>備註  
 **OPENQUERY** 提供更安全的方式來存取外部資料，方法是支援資料來源許可權。 因為連接字串儲存在資料來源中，所以管理員可以使用資料來源的屬性管理資料的存取。 如需資料來源的詳細資訊，請參閱 [&#40;SSAS-多維度&#41;支援的資料來源 ](/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional)。  
  
 您可以藉由查詢 **MDSCHEMA_INPUT_DATASOURCES** 架構資料列集，取得可在伺服器上使用的資料來源清單。 如需使用 **MDSCHEMA_INPUT_DATASOURCES**的詳細資訊，請參閱 MDSCHEMA_INPUT_DATASOURCES 資料列 [集](/previous-versions/sql/sql-server-2012/ms126243(v=sql.110))。  
  
 您也可以使用下列 DMX 查詢，傳回目前 Analysis Services 資料庫中的資料來源清單：  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>範例  
 下列範例會使用已經在資料庫中定義的 MyDS 資料來源 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 來建立資料庫的連接 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] ，並查詢 **vTargetMail** view。  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#60;來源資料查詢&#62;](../dmx/source-data-query.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
