---
title: 為悖論創建索引 |微軟文件
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
ms.openlocfilehash: 2e68484efdc5194f93f2acab31973377d9c66f1c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280908"
---
# <a name="create-index-for-paradox"></a>Paradox 的 CREATE INDEX
ODBC 悖論驅動程式的 CREATE INDEX 語句的語法是:  
  
 **建立**=**唯一**=**索引***索引名稱*  
  
 **開啟***表名*  
  
 **(***列識別碼*=**ASC**|  
  
 【**,** *列識別子*】**ASC**= ...**)**  
  
 ODBC 悖論驅動程式不支援 CREATE INDEX 語句的 ODBC SQL 語法中的**DESC**關鍵字。 *表名稱*參數可以指定表的完整路徑。  
  
 如果指定了關鍵字**UNIQUE,** 則 ODBC 悖論驅動程式將創建一個唯一索引。 第一個唯一索引創建為主索引。 這是一個名為*表名的*Paradox主鍵檔。Px。 主要索引受以下限制:  
  
-   必須先創建主索引,然後才能將任何行添加到表中。  
  
-   主索引必須定義在表中的第一個"n"列上。  
  
-   每個表只允許一個主索引。  
  
-   如果未在表上定義主索引,則 Paradox 驅動程式無法更新表。 (請注意,對於空表,這不是真的,即使表上未定義唯一索引,也可以更新空錶。  
  
-   主索引的*索引名稱*參數必須與表的基名相同,這是 Paradox 的要求。  
  
 如果省略關鍵字**UNIQUE**UNIQUE,ODBC 悖論驅動程式將創建一個非唯一索引。 這包括兩個稱為*表名*的 Paradox 輔助索引檔。X*nn*與*表名*。Y*nn*,其中*nn*是表中列的編號。 非唯一索引受以下限制:  
  
-   在為表創建非唯一索引之前,該表必須存在主索引。  
  
-   對於悖論3。*x*,主索引(唯一或非唯一)以外的任何索引*的索引名稱*參數必須與列名稱相同。 對於悖論4。*x*和 5。*x*,此類索引的名稱可以是,但不必與列名稱相同。  
  
-   只能為非唯一索引指定一列。  
  
 在表上定義索引後,無法添加列。 如果 CREATE TABLE 語句的參數清單的第一列建立索引,則第二列不能包含在參數清單中。  
  
 例如,要使用銷售訂單號和行號列作為SO_LINES表上的唯一索引,請使用語句:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 要將零件號列用作SO_LINES表上的非唯一索引,請使用語句:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 請注意,執行兩個 CREATE INDEX 語句時,第一個語句將始終創建與表同名的主索引,第二個語句將始終創建與列同名的非唯一索引。 即使在 CREATE INDEX 語句中輸入了不同的名稱,並且索引在第二個 CREATE INDEX 語句中標記為 UNIQUE,也會以這種方式命名這些索引。  
  
> [!NOTE]  
>  當您在不實現 Borland 資料庫引擎的情況下使用 Paradox 驅動程式時,只允許讀取和追加語句。
