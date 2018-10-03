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
manager: craigg
ms.openlocfilehash: 66dab60f4a9a180d2a8b74ce4d0c8f4d7bf8d242
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682836"
---
# <a name="dbase-indexes"></a>dBASE 索引
ODBC dBASE 驅動程式會自動開啟，並更新 dBASE IV 索引檔案。 您必須使用**選取索引**顯示透過 ODBC 資料來源管理員 dBASE 檔案相關聯 dBASE III.ndx 檔案對話方塊。  
  
 下列限制適用於建立 dBASE 索引：  
  
-   所有的資料行名稱必須是有效的。  
  
-   所有資料行必須位於相同的遞增或遞減的順序而定。  
  
-   任何單一文字資料行的長度必須少於 100 個位元組。  
  
-   有多個資料行時，所有資料行必須是文字資料行和資料行大小的總和必須小於 100 個位元組。  
  
-   附註欄位無法編製索引。  
  
-   索引不得指定欄位的最新的集合 （也就是不允許重複的索引）。  
  
-   索引名稱必須符合 dBASE 索引命名慣例。 dBASE III 要求每個索引必須在個別的檔案中，每個皆具有.ndx 延伸模組。 DBASE IV，在建立索引做為儲存在單一.mdx 檔案的標記名稱。 .Mdx 檔案具有相同的基底名稱與資料庫檔案 （例如 Emp.mdx 是 Emp.dbf 資料庫的索引檔）。  
  
-   dBASE 定義唯一索引做為其中一個只有一筆記錄，從相同金鑰值組加入至索引的位置。
