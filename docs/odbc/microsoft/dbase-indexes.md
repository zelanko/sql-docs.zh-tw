---
description: dBASE 索引
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 30a6390f0e187cc063b2a650af2da3b9fcc87d57
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340954"
---
# <a name="dbase-indexes"></a>dBASE 索引
ODBC dBASE 驅動程式會自動開啟，並更新 dBASE IV 索引檔案。 您必須使用透過「ODBC 資料來源管理員」顯示的 [ **選取索引** ] 對話方塊，將 dbase ndx 檔案與 dbase 檔案產生關聯。  
  
 下列限制適用于建立 dBASE 索引：  
  
-   所有資料行名稱都必須是有效的。  
  
-   所有資料行的遞增或遞減順序都必須相同。  
  
-   任何單一文字資料行的長度都必須小於100個位元組。  
  
-   如果有一個以上的資料行存在，則所有資料行都必須是文字資料行，而且資料行大小的總和必須小於100個位元組。  
  
-   無法為備忘錄欄位編制索引。  
  
-   不得為目前的欄位集合指定索引 (也就是說，不允許重複的索引) 。  
  
-   索引名稱必須符合 dBASE 索引命名慣例。 dBASE III 要求每個索引都位於個別的檔案中，每個都有副檔名為 ndx 的檔案。 在 dBASE IV 中，索引會建立為儲存在單一 mdx 檔案中的標記名稱。 Mdx 檔案的基底名稱與資料庫檔案的基底名稱相同 (例如，Emp 是用於 Emp 資料庫) 的索引檔。  
  
-   dBASE 將唯一索引定義為一個唯一的索引，其中一個索引鍵值相同的集合中的一筆記錄會新增至索引。
