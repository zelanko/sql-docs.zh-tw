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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1333cd6cd5946b7a3a70152e12f4d3decfa7fed0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138426"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 陳述式限制
使用 dBASE 或 Paradox 驅動程式時，一旦建立索引並加入新記錄之後，ALTER TABLE 語句就無法變更資料表的結構，除非卸載索引並刪除資料表的內容。  
  
 Microsoft Excel 或文字驅動程式不支援 ALTER TABLE 語句。  
  
> [!NOTE]  
>  當您使用 Paradox 驅動程式，但未執行 Borland 資料庫引擎時，不支援 ALTER TABLE 語句;只允許 read 和 append 語句。
