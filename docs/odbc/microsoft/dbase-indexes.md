---
title: "dBASE 索引 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b71b043667708c69494d5b057436f35b7d1a288d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="dbase-indexes"></a>dBASE 索引
ODBC dBASE 驅動程式會自動開啟，並更新 dBASE IV 索引檔案。 您必須使用**選取索引**顯示透過 ODBC 資料來源管理員與 dBASE 檔案中的 dBASE III.ndx 檔案對話方塊。  
  
 下列限制適用於建立 dBASE 索引：  
  
-   所有資料行名稱必須是有效的。  
  
-   所有資料行必須以相同的遞增或遞減順序。  
  
-   任何單一文字資料行的長度必須小於 100 個位元組。  
  
-   如果多個資料行存在，所有資料行必須是文字資料行和資料行大小的總和必須小於 100 個位元組。  
  
-   附註欄位無法編製索引。  
  
-   不得指定目前的資料集欄位的索引 （也就是說，不允許重複的索引）。  
  
-   索引名稱必須符合 dBASE 索引命名慣例。 dBASE III 要求每個索引必須在個別的檔案中，每個皆.ndx 擴充功能。 DBASE IV，在建立索引做為儲存在單一.mdx 檔案的標記名稱。 .mdx 檔具有相同的基底名稱和資料庫檔案 （例如，Emp.mdx 是 Emp.dbf 資料庫索引檔）。  
  
-   dBASE 定義唯一索引為只有一筆記錄，從相同的金鑰值組加入至索引的位置。
