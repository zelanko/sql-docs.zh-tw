---
title: Paradox 的 CREATE INDEX |Microsoft Docs
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
ms.openlocfilehash: 331613676b748453a56da1e41fe85f04a7715038
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081943"
---
# <a name="create-index-for-paradox"></a>Paradox 的 CREATE INDEX
ODBC Paradox 驅動程式之 CREATE INDEX 語句的語法為：  
  
 **建立**[**唯一**]**索引***索引-名稱*  
  
 **在***資料表名稱*上  
  
 **（** 資料*行識別碼*[**ASC**]  
  
 [**，** 資料*行識別碼*[**ASC**] ...]**)**  
  
 在 ODBC SQL 文法中，ODBC Paradox 驅動程式不支援 CREATE INDEX 語句的**DESC**關鍵字。 *資料表名稱*引數可以指定資料表的完整路徑。  
  
 如果指定了關鍵字**UNIQUE** ，則 ODBC Paradox 驅動程式會建立唯一的索引。 第一個唯一索引會建立為主要索引。 這是名為 [*資料表名稱*] 的 Paradox 主要金鑰檔案。圖元. 主要索引受限於下列限制：  
  
-   在將任何資料列加入資料表之前，必須先建立主要索引。  
  
-   必須在資料表中的第一個 "n" 資料行上定義主要索引。  
  
-   每個資料表只允許一個主要索引。  
  
-   如果未在資料表上定義主要索引，則 Paradox 驅動程式無法更新資料表。 （請注意，空白資料表的這種情況並不適用，即使資料表上未定義唯一索引，也可以更新）。  
  
-   主要索引的*索引名稱*引數必須與資料表的基底名稱相同，因為 Paradox 的要求。  
  
 如果省略關鍵字**UNIQUE** ，則 ODBC Paradox 驅動程式會建立非唯一的索引。 這是由兩個名為 [*資料表名稱*] 的 Paradox 次要索引檔所組成。X*nn*和*資料表名稱*。Y*nn*，其中*nn*是資料表中的資料行數目。 非唯一索引會受到下列限制：  
  
-   在建立資料表的非唯一索引之前，該資料表必須有主要索引。  
  
-   適用于 Paradox 3。*x*，主要索引以外的任何索引（唯一或非唯一）的*索引名稱*引數必須與資料行名稱相同。 適用于 Paradox 4。*x*和5。*x*，這類索引的名稱可以是，但不一定要與資料行名稱相同。  
  
-   只能為非唯一索引指定一個資料行。  
  
 一旦在資料表上定義索引之後，就無法加入資料行。 如果 CREATE TABLE 語句之引數清單的第一個資料行建立索引，第二個數據行就不能包含在引數清單中。  
  
 例如，若要使用「銷售訂單號碼」和「行號」資料行做為 SO_LINES 資料表上的唯一索引，請使用語句：  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 若要使用 [元件編號] 資料行做為 SO_LINES 資料表上的非唯一索引，請使用語句：  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 請注意，當執行兩個 CREATE INDEX 語句時，第一個語句一律會使用與資料表相同的名稱來建立主要索引，而第二個語句一律會建立與資料行名稱相同的非唯一索引。 即使在 CREATE INDEX 語句中輸入不同的名稱，以及在第二個 CREATE INDEX 語句中將索引標示為 UNIQUE，這些索引還是會以這種方式命名。  
  
> [!NOTE]  
>  當您使用 Paradox 驅動程式，但未執行 Borland 資料庫引擎時，只允許 read 和 append 語句。
