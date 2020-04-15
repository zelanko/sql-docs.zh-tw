---
title: dBASE 指數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9300a38a0e36da771a238f73b77d3dda527334ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307669"
---
# <a name="dbase-indexes"></a>dBASE 索引
ODBC dBASE 驅動程式自動打開並更新 dBASE IV 索引檔。 您必須使用透過 ODBC 資料來源管理員顯示**的「選擇索引」** 對話方塊將 dBASE III .ndx 檔與 dBASE 檔案相關聯。  
  
 以下限制適用於 dBASE 索引的建立:  
  
-   所有列名稱必須有效。  
  
-   所有列必須以相同的升序或降冪排列。  
  
-   任何單個文本列的長度必須小於 100 位元組。  
  
-   如果存在多個列,則所有列都必須為文本列,並且列大小的總和必須小於 100 位元組。  
  
-   無法對備忘錄欄位進行索引。  
  
-   不得為當前欄位集指定索引(即不允許重複索引)。  
  
-   索引名稱必須與 dBASE 索引命名約定匹配。 dBASE III 要求每個索引位於一個單獨的檔中,每個索引都有一個 .ndx 擴展名。 在 dBASE IV 中,索引創建為存儲在單個 .mdx 檔案中的標記名稱。 .mdx 檔案與資料庫檔具有相同的基本名稱(例如,Emp.mdx 是 Emp.dbf 資料庫的索引檔)。  
  
-   dBASE 將唯一索引定義為在索引中僅將具有相同鍵值集中的一條記錄添加到索引中。
