---
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
ms.openlocfilehash: 19afa8b07b0051de9ce45ec652ea337c0f689f52
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304697"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 陳述式限制
使用 dBASE 或 Paradox 驅動程式時，一旦建立索引並加入新記錄之後，ALTER TABLE 語句就無法變更資料表的結構，除非卸載索引並刪除資料表的內容。  
  
 Microsoft Excel 或文字驅動程式不支援 ALTER TABLE 語句。  
  
> [!NOTE]  
>  當您使用 Paradox 驅動程式，但未執行 Borland 資料庫引擎時，不支援 ALTER TABLE 語句;只允許 read 和 append 語句。
