---
title: "OPENROWSET (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: OPENROWSET
dev_langs: DMX
helpviewer_keywords: OPENROWSET statement
ms.assetid: 8c8b61b4-2bf6-46c7-8976-51484004dc22
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a95fc508806d4653228caf5a72bac0109646a5f8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
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
 資料採礦提供者會連接到資料來源物件使用*provider_name*和*provider_string，* ，且會執行指定的查詢*query_syntax*來源資料中擷取資料列集。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [&#60; 來源資料查詢 &#62;](../dmx/source-data-query.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
