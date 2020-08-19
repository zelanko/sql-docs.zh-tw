---
description: Paradox 的 CREATE INDEX
title: 建立 Paradox 的索引 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0274f3f7cfdb79bf64e3616b16b7f3383063e07
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483641"
---
# <a name="create-index-for-paradox"></a>Paradox 的 CREATE INDEX
ODBC Paradox 驅動程式之 CREATE INDEX 語句的語法如下：  
  
 **建立**[**唯一**]**索引***索引名稱*  
  
 **在***資料表名稱*上  
  
 ** (** 資料 *行識別碼* [**ASC**]  
  
 [**，** 資料 *行識別碼* [**ASC**] ...]**) **  
  
 ODBC Paradox 驅動程式不支援 ODBC SQL 文法中 CREATE INDEX 語句的 **DESC** 關鍵字。 *資料表名稱*引數可以指定資料表的完整路徑。  
  
 如果指定了 **unique** 關鍵字，ODBC Paradox 驅動程式將會建立唯一索引。 第一個唯一索引會建立為主要索引。 這是名為 [ *資料表名稱*] 的 Paradox 主要金鑰檔。Px。 主要索引受到下列限制：  
  
-   在將任何資料列新增至資料表之前，必須先建立主要索引。  
  
-   主要索引必須定義在資料表中的第一個 "n" 資料行上。  
  
-   每個資料表只允許一個主要索引。  
  
-   如果未在資料表上定義主要索引，Paradox 驅動程式就無法更新資料表。  (請注意，空的資料表不是如此，即使資料表上未定義唯一索引，也可以更新此值。 )   
  
-   主要索引的 *索引名稱* 引數必須與資料表的基底名稱相同，因為 Paradox 的要求。  
  
 如果省略 **unique** 關鍵字，ODBC Paradox 驅動程式將會建立非唯一的索引。 這包含兩個名為 [ *資料表名稱*] 的 Paradox 次要索引檔。X*nn* 和 *資料表名稱*。Y*nn*，其中 *nn* 是資料表中的資料行數目。 非唯一索引會受到下列限制：  
  
-   在可以為資料表建立非唯一索引之前，該資料表必須有主要索引。  
  
-   若為 Paradox 3。*x*， (唯一或非唯一的) 之索引的 *索引名稱* 引數，必須與資料行名稱相同。 若為 Paradox 4。*x* 和5。*x*，這類索引的名稱可以是，但不一定要與資料行名稱相同。  
  
-   只有一個資料行可以指定為非唯一索引。  
  
 一旦資料表上已定義索引，就無法加入資料行。 如果 CREATE TABLE 語句的引數清單的第一個資料行建立索引，則第二個數據行不能包含在引數清單中。  
  
 例如，若要使用「銷售訂單編號」和「行號」資料行做為 SO_LINES 資料表上的唯一索引，請使用下列語句：  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 若要使用 [元件編號] 資料行做為 SO_LINES 資料表上的非唯一索引，請使用語句：  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 請注意，當執行兩個 CREATE INDEX 語句時，第一個語句一律會使用與資料表相同的名稱來建立主要索引，而第二個語句一律會使用與資料行相同的名稱建立非唯一的索引。 即使在 CREATE INDEX 語句中輸入不同的名稱，即使在第二個 CREATE INDEX 語句中將索引標示為 UNIQUE，這些索引仍會以這種方式命名。  
  
> [!NOTE]  
>  當您使用 Paradox 驅動程式但未執行 Borland 資料庫引擎時，只允許讀取和附加語句。
