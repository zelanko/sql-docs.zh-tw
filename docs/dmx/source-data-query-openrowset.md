---
title: OPENROWSET (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8be3fe8cbf30121ec2895f59306c925a422d5c39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938129"
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;來源資料查詢&gt;-OPENROWSET
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  以對外部提供者的查詢取代來源資料查詢。 INSERT、 SELECT FROM PREDICTION JOIN，和 SELECT FROM NATURAL PREDICTION JOIN 陳述式支援**OPENROWSET**。  
  
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
 資料採礦提供者會連接到資料來源物件使用*provider_name*並*provider_string，* 並將執行中指定的查詢*query_syntax*來擷取來源資料中的資料列集。  
  
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
 [資料採礦延伸模組&#40;DMX&#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
