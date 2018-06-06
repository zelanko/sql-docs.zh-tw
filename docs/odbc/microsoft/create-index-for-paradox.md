---
title: 建立索引的 Paradox |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 473c8d73e33504e7cc22d3b02aaca789d9c7a620
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="create-index-for-paradox"></a>建立索引的 Paradox
ODBC Paradox 驅動程式的 CREATE INDEX 陳述式的語法為：  
  
 **建立**[**UNIQUE**]**索引***索引名稱*  
  
 **ON** *資料表名稱*  
  
 **(** *資料行識別碼*[**ASC**]  
  
 [**，** *資料行識別碼*[**ASC**]...]**)**  
  
 ODBC Paradox 驅動程式不支援**DESC** CREATE INDEX 陳述式的 ODBC SQL 文法中的關鍵字。 *資料表名稱*引數可以指定資料表的完整路徑。  
  
 如果關鍵字**UNIQUE**指定，則 ODBC Paradox 驅動程式會建立唯一索引。 第一個唯一的索引會建立為主要的索引。 這是 Paradox 主要金鑰檔名為*資料表名稱*。像素。 主要索引受限於下列限制：  
  
-   任何資料列加入至資料表之前，必須建立主索引鍵。  
  
-   在資料表中的第一個"n"資料行時都必須定義主索引鍵。  
  
-   每個資料表允許只能有一個主要的索引。  
  
-   Paradox 驅動程式無法更新資料表，如果資料表上未定義主索引鍵。 （請注意這不是空的資料表，即使未在資料表上定義唯一索引可更新的則為 true）。  
  
-   *索引名稱*做為主要索引的引數必須是相同基底資料表的名稱、 所需的 Paradox。  
  
 如果關鍵字**UNIQUE**已省略，則為 ODBC Paradox 驅動程式會建立非唯一的索引。 這包含兩個 Paradox 次要索引檔案命名為*資料表名稱*。X*nn*和*資料表名稱*。Y*nn*，其中*nn*是資料表中的資料行的數目。 非唯一索引受限於下列限制：  
  
-   非唯一的索引可以建立資料表之前，該資料表必須存在主要的索引。  
  
-   如 Paradox 3。*x*、*索引名稱*主要的索引 （唯一或非唯一） 以外的任何索引的引數必須是相同的資料行名稱。 如 Paradox 4。*x*和 5。*x*，這類索引的名稱，但不一定要是資料行名稱相同。  
  
-   只有一個資料行可以指定為非唯一索引。  
  
 一旦已定義索引的資料表上，無法加入資料行。 如果 CREATE TABLE 陳述式的引數清單的第一個資料行建立索引，第二個資料行不會包含引數清單中。  
  
 例如，若要使用銷售訂單號碼和行數字資料行做為 SO_LINES 資料表上唯一的索引，使用陳述式：  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 若要使用部分的數字資料行做為 SO_LINES 資料表上的非唯一索引，使用陳述式：  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 請注意，兩個 CREATE INDEX 陳述式執行時，第一個陳述式一律會建立具有相同名稱做為資料表的主要索引的第二個陳述式具有相同名稱的資料行一律會建立非唯一的索引。 即使在 CREATE INDEX 陳述式中輸入不同的名稱，且索引會標示為唯一的第二個 CREATE INDEX 陳述式中，這些索引會命名這種方式。  
  
> [!NOTE]  
>  當您使用 Paradox 驅動程式，而不需要實作 Borland Database Engine，只能讀取和附加，允許陳述式。
