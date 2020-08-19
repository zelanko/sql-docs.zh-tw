---
description: ALTER TABLE 陳述式限制
title: ALTER TABLE 語句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53f86e8d2c21fb6ea2d016610848773564d4a384
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449590"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 陳述式限制
使用 dBASE 或 Paradox 驅動程式時，一旦建立索引並加入新的記錄之後，ALTER TABLE 語句就無法變更資料表的結構，除非卸載索引並刪除資料表的內容。  
  
 Microsoft Excel 或文字驅動程式不支援 ALTER TABLE 語句。  
  
> [!NOTE]  
>  當您在未執行 Borland 資料庫引擎的情況下使用 Paradox 驅動程式時，不支援 ALTER TABLE 語句;只允許讀取和附加語句。
