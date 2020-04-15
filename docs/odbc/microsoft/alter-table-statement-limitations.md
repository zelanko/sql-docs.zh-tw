---
title: 變更表語句限制 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304697"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 陳述式限制
使用 dBASE 或 Paradox 驅動程式時,建立索引並添加新記錄後,ALTER TABLE 語句無法更改表的結構,除非刪除索引並刪除表的內容。  
  
 Microsoft Excel 或文字驅動程式不支援 ALTER TABLE 語句。  
  
> [!NOTE]  
>  當您在不實現 Borland 資料庫引擎的情況下使用 Paradox 驅動程式時,不支援 ALTER TABLE 語句;因此,如果不執行「不帶悖論」,則不支援 ALTER TABLE 語句。僅允許讀取和追加語句。
