---
description: '&lt;來源資料查詢 &gt; -OPENROWSET'
title: OPENROWSET (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8da3686e7772b7e997690d509c8092917635497a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500760"
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;來源資料查詢 &gt; -OPENROWSET
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  以對外部提供者的查詢取代來源資料查詢。 INSERT、SELECT FROM 預測聯結，以及 SELECT FROM 自然預測聯結語句支援 **OPENROWSET**。  
  
## <a name="syntax"></a>語法  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>引數  
 *provider_name*  
 OLE DB 提供者名稱。  
  
 *provider_string*  
 指定之提供者的 OLE DB 連接字串。  
  
 *query_syntax*  
 傳回資料列集的查詢語法。  
  
## <a name="remarks"></a>備註  
 資料採礦提供者會使用 *provider_name* 和 provider_string 來建立與資料來源物件的連接 *，* 並會執行 *query_syntax* 中指定的查詢，以從來源資料取出資料列集。  
  
## <a name="examples"></a>範例  
 下列範例可以用在 PREDICTION JOIN 陳述式中，使用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] SELECT 陳述式從 [!INCLUDE[tsql](../includes/tsql-md.md)] 資料庫擷取資料。  
  
```  
OPENROWSET  
(  
'SQLOLEDB.1',  
'Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security     Info=False;Initial Catalog=AdventureWorksDW2012;Data Source=localhost',  
'SELECT TOP 1000 * FROM vTargetMail'  
)  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#60;來源資料查詢&#62;](../dmx/source-data-query.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
