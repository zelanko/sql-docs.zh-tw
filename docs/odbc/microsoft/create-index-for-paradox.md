---
title: CREATE INDEX for Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15e16fb311bf3c9acb2823772247e0fc16eabeef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232305"
---
# <a name="create-index-for-paradox"></a>Paradox 的 CREATE INDEX
CREATE INDEX 陳述式，ODBC Paradox 驅動程式的語法是：  
  
 **CREATE** [**UNIQUE**] **INDEX** *index-name*  
  
 **ON** *table-name*  
  
 **(** *column-identifier* [**ASC**]  
  
 [ **,** *column-identifier* [**ASC**]...] **)**  
  
 ODBC Paradox 驅動程式不支援**DESC** CREATE INDEX 陳述式的 ODBC SQL 文法中的關鍵字。 *資料表名稱*引數可以指定資料表的完整路徑。  
  
 如果關鍵字**UNIQUE**指定時，ODBC Paradox 驅動程式會建立唯一索引。 第一個唯一的索引會建立為主要的索引。 這是 Paradox 主索引鍵名稱為的檔案*資料表名稱*。像素。 主要索引受限於下列限制：  
  
-   任何資料列加入至資料表之前，必須建立主索引鍵。  
  
-   在資料表中的第一個"n"資料行時，必須定義主要索引。  
  
-   每個資料表允許只有一個主要的索引。  
  
-   Paradox 驅動程式無法更新資料表，如果資料表上未定義主索引鍵。 （請注意，這不是空的資料表，即使未在資料表上定義唯一索引可以更新，則為 true）。  
  
-   *的索引名稱*主要索引的引數必須是基底資料表，所需的 Paradox 的名稱相同。  
  
 如果關鍵字**UNIQUE**已省略，ODBC Paradox 驅動程式會建立非唯一的索引。 這兩個名為 Paradox 次要索引檔案所組成*資料表名稱*。X*nn*並*資料表名稱*。Y*nn*，其中*nn*是資料表中的資料行的數目。 非唯一索引受限於下列限制：  
  
-   非唯一索引可以建立資料表之前，該資料表必須存在主要的索引。  
  
-   針對 Paradox 3。*x*，則*的索引名稱*任何索引，而不是主要的索引 （唯一或非唯一） 的引數必須是相同的資料行名稱。 針對 Paradox 4。*x*和 5。*x*，這類索引的名稱，但不一定要是資料行名稱相同。  
  
-   只有一個資料行可以指定為非唯一的索引。  
  
 在資料表上定義索引之後，就無法加入資料行。 如果 CREATE TABLE 陳述式的引數清單的第一個資料行建立索引，第二個資料行不能包含引數清單中。  
  
 例如，若要使用的銷售訂單號碼行數字資料行做為 SO_LINES 資料表上唯一的索引，使用陳述式：  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 若要使用部分的數字資料行上 SO_LINES 資料表的非唯一索引，使用此陳述式：  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 請注意，兩個 CREATE INDEX 陳述式執行時，第一個陳述式一律會建立具有相同名稱做為資料表的主索引鍵的第二個陳述式一律會建立具有相同名稱的資料行的非唯一的索引。 這些索引將會命名為如此一來即使 CREATE INDEX 陳述式中輸入不同的名稱，且索引會標示為唯一的第二個 CREATE INDEX 陳述式中。  
  
> [!NOTE]  
>  當您使用 Paradox 驅動程式，而不需要實作 Borland Database Engine，只能讀取，並附加允許陳述式。
