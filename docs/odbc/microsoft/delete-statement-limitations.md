---
title: DELETE 子句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eb2587f733f5042436144f7865627fee576e3d9c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096316"
---
# <a name="delete-statement-limitations"></a>DELETE 陳述式限制
Microsoft Excel 或文字驅動程式不支援 DELETE 子句。 請注意，Text 驅動程式支援 INSERT 語句。  
  
 DBASE 驅動程式不支援封裝資料表來移除「已刪除」的值。  
  
 若要讓 Paradox 驅動程式從資料表中刪除資料列，資料表必須有唯一的索引（Paradox 主鍵）。
