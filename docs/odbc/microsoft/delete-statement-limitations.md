---
title: DELETE 陳述式的限制 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caa4855c83815c8876c4674bf01de3f9c4bd4231
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32898853"
---
# <a name="delete-statement-limitations"></a>刪除陳述式的限制
DELETE 陳述式不支援 Microsoft Excel 或文字驅動程式。 請注意，文字驅動程式支援 INSERT 陳述式。  
  
 DBASE 驅動程式不支援壓縮資料表來移除 「 刪除 」 的值。  
  
 Paradox 驅動程式從資料表刪除資料列時，該資料表必須有唯一的索引 （Paradox 主索引鍵）。
