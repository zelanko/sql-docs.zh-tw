---
title: FOR XML AUTO 查詢會傳回衍生的資料表參考在 90 或之後的相容性模式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- FOR XML AUTO [SQL Server]
ms.assetid: 10c32f06-f7e1-40e0-8f79-6d921f2bef1d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84e00a2111b9cfe38ca680ec6c17ada724456878
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62503706"
---
# <a name="for-xml-auto-queries-return-derived-table-references-in-90-or-later-compatibility-modes"></a>FOR XML AUTO 查詢在 90 或之後的相容性模式中，會傳回衍生的資料表參考
  當資料庫相容性層級設定為 90 或之後時，在 AUTO 模式中執行的 FOR XML 查詢會傳回衍生資料表別名的參考。 當相容性層級設定為 80 時，FOR XML AUTO 查詢會傳回定義衍生資料表之基底資料表的參考。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 例如，請考慮下表：  
  
```  
CREATE TABLE Test(id int);  
INSERT INTO Test VALUES(1);  
INSERT INTO Test VALUES(2);  
```  
  
 下列查詢 (包括衍生資料表) 會在不同的相容性層級 (80、90 或之後) 底下產生不同的結果：  
  
```  
SELECT * FROM   
   (SELECT a.id AS a, b.id AS b   
    FROM Test a JOIN Test b ON a.id=b.id)  
AS DerivedTest   
FOR XML AUTO;  
```  
  
 在相容性層級 80 底下，此查詢會傳回下列結果。 結果會參考衍生資料表的基底資料表別名 `a` 和 `b` 而非衍生資料表別名。  
  
```  
<a a="1"><b b="1"/></a><a a="2"><b b="2"/></a>  
```  
  
 在相容性層級 90 或之後底下，此查詢會傳回衍生資料表別名的參考 `DerivedTest` 而非衍生資料表之基底資料表的參考。  
  
```  
<DerivedTest a="1" b="1"/><DerivedTest a="2" b="2"/>  
```  
  
## <a name="corrective-action"></a>更正動作  
 視需要修改您的應用程式，以便將包含衍生資料表且在相容性層級 90 或之後底下執行之 FOR XML AUTO 查詢所導致的變更納入考量。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
