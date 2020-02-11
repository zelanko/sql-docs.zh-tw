---
title: ORDER BY 子句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ORDER BY clause limitations
- ORDER BY clause limitations [ODBC]
ms.assetid: fd4ddc7c-9c7e-4a0c-a781-e5427dfb2e18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b58afff444c09622027f50a87bd77fcd6ed45640
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100785"
---
# <a name="order-by-clause-limitations"></a>ORDER BY 子句限制
如果 SELECT 語句包含 GROUP BY 子句和 ORDER BY 子句，ORDER BY 子句只能包含結果集內的資料行或 GROUP BY 子句中的運算式。
