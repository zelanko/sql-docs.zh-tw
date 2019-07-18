---
title: 圖形 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c928d4c96917479f8c37415d5ebe2db9b7f9eb98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938110"
---
# <a name="ltsource-data-querygt---shape"></a>&lt;來源資料查詢&gt;-圖形
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  將多個資料來源的查詢結合到單一階層式資料表 (亦即，有巢狀資料表的資料表)，這個資料表會成為採礦模型的案例資料表。  
  
 完整的語法**形狀**命令會記載在[!INCLUDE[msCoName](../includes/msconame-md.md)]Data Access Components (MDAC) 軟體開發套件 (SDK)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SHAPE {<master query>}  
APPEND ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS < column table name>  
...  
]       
```  
  
## <a name="arguments"></a>引數  
 *主要的查詢*  
 傳回父資料表的查詢。  
  
 *子資料表查詢*  
 傳回巢狀資料表的查詢。  
  
 *主要的資料行*  
 父資料表中，識別子資料表查詢結果中之子資料列的資料行。  
  
 *子資料行*  
 子資料表中，識別主要查詢結果中之父資料列的資料行。  
  
 *資料行的資料表名稱*  
 巢狀資料表中，父資料表內新附加的資料行名稱。  
  
## <a name="remarks"></a>備註  
 您必須根據會建立父資料表與子資料表之關聯性的資料行來排序查詢。  
  
## <a name="examples"></a>範例  
 您可以使用下列範例中的[插入&#40;DMX&#41; ](../dmx/insert-into-dmx.md)陳述式來定型包含巢狀的資料表的模型。 兩個資料表內**形狀**陳述式透過相關聯**OrderNumber**資料行。  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>另請參閱  
 [&#60;來源資料查詢&#62;](../dmx/source-data-query.md)   
 [資料採礦延伸模組&#40;DMX&#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組&#40;DMX&#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
