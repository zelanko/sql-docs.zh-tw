---
title: 形成傳回之 XML 的 AUTO 模式啟發學習法 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, heuristics in shaping returned XML
ms.assetid: 6c5cb6c1-2921-4ba1-8100-0bf8074f9103
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff27ed7bdfc7554fd68f65f8efd257731cbe09a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757486"
---
# <a name="auto-mode-heuristics-in-shaping-returned-xml"></a>用來形成傳回之 XML 的 AUTO 模式啟發式方法
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  AUTO 模式可依據查詢來決定所傳回之 XML 的外觀。 在決定如何將元素進行巢狀化時，AUTO 模式啟發式方法會比較相鄰資料列中的資料行值。 除了 **ntext**、 **text**、 **image**和 **xml**之外，所有類型的資料行都會加以比較。 **(n)varchar(max)** 和 **varbinary(max)** 類型的資料行也會比較。  
  
 下列範例說明用來決定所產生之 XML 外觀的 AUTO 模式啟發式方法：  
  
```  
SELECT T1.Id, T2.Id, T1.Name  
FROM   T1, T2  
WHERE ...  
FOR XML AUTO  
ORDER BY T1.Id  
```  
  
 在決定新的 <`T1`> 元素要從哪裡開始時，若沒有指定 T1 資料表上的索引鍵，就會比較 T1 的所有資料行值 (**ntext**、**text**、**image** 和 **xml** 除外)。 接著，假設 **Name** 資料行是 **nvarchar(40)**，且 SELECT 陳述式傳回下列資料列集：  
  
```  
T1.Id  T1.Name  T2.Id  
-----------------------  
1       Andrew    2  
1       Andrew    3  
1       Nancy     4  
```  
  
 AUTO 模式啟發式方法會比較 T1 資料表中，Id 及 Name 資料行的所有值。 因為前兩個資料列的 ID 及 Name 資料行具有相同值，因此結果中會新增一個具有兩個 \<T2> 子項目的 \<T1> 項目。  
  
 以下是所傳回的 XML：  
  
```  
<T1 Id="1" Name="Andrew">  
    <T2 Id="2" />  
    <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
      <T2 Id="4" />  
</T>  
```  
  
 現在，假設 Name 資料行的類型為 **text** 。 AUTO 模式啟發式方法不會比較此類型的值， 反之，它會假設這些值都不一樣。 所產生的 XML 結果如下所示：  
  
```  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="2" />  
</T1>  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
  <T2 Id="4" />  
</T1>  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 AUTO 模式](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
