---
title: ALTER TABLE 陳述式限制 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 02ce530385cdc911250a81d831dd2fdb81873f76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301980"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 陳述式限制
DBASE 或 Paradox 驅動程式會使用時，在建立索引，並新增新的記錄，無法由 ALTER TABLE 陳述式變更資料表的結構，除非卸除索引和資料表的內容會被刪除之後。  
  
 Microsoft Excel 或文字的驅動程式不支援 ALTER TABLE 陳述式。  
  
> [!NOTE]  
>  當您使用 Paradox 驅動程式而不需要實作 Borland Database Engine 時，不支援 ALTER TABLE 陳述式;僅讀取和附加允許陳述式。
