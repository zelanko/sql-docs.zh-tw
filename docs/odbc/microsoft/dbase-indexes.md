---
title: dBASE 索引 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9a0a57c3dce920c6d5fbc2510932066cb5a2659
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096363"
---
# <a name="dbase-indexes"></a>dBASE 索引
ODBC dBASE 驅動程式會自動開啟並更新 dBASE IV 索引檔案。 您必須使用透過 ODBC 資料來源管理員顯示的 [**選取索引**] 對話方塊，將 dbase III. ndx 檔案與 dbase 檔案產生關聯。  
  
 下列限制適用于建立 dBASE 索引：  
  
-   所有資料行名稱都必須是有效的。  
  
-   所有資料行都必須是相同的遞增或遞減順序。  
  
-   任何單一文字資料行的長度都必須小於100個位元組。  
  
-   如果有一個以上的資料行存在，所有資料行都必須是文字資料行，而且資料行大小的總和必須小於100個位元組。  
  
-   無法為備忘欄位編制索引。  
  
-   不得為目前的欄位集合指定索引（也就是不允許重複的索引）。  
  
-   索引名稱必須符合 dBASE 索引命名慣例。 dBASE III 要求每個索引都位於個別的檔案中，每個都有 ndx 副檔名。 在 dBASE IV 中，會將索引建立成儲存在單一 mdx 檔案中的標記名稱。 此 mdx 檔案的基底名稱與資料庫檔案相同（例如，Emp 是 Emp 資料庫的索引檔案）。  
  
-   dBASE 會將唯一索引定義為一個，其中只有一個具有相同索引鍵值的集合中的記錄，才會新增至索引。
