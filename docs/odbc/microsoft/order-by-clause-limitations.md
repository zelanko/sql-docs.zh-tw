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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e80fcf8b1f2e3e83182e3278b63bdb856c7189fe
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292928"
---
# <a name="order-by-clause-limitations"></a>ORDER BY 子句限制
如果 SELECT 語句包含 GROUP BY 子句和 ORDER BY 子句，ORDER BY 子句只能包含結果集內的資料行或 GROUP BY 子句中的運算式。
