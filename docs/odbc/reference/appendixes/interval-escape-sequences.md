---
title: 間隔逸出序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81481db74d973da0e54bc6bf9e70550fa3cc0c81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188893"
---
# <a name="interval-escape-sequences"></a>間隔逸出序列
ODBC 會將逸出序列用於間隔常值。 此逸出序列的語法如下所示：  
  
 {*interval-literal*}  
  
 Backus-naur form，BNF 語法*間隔 string-literal*，請參閱[間隔常值語法](../../../odbc/reference/appendixes/interval-literal-syntax.md)稍後本附錄一節。  
  
 如果資料來源所支援間隔資料類型，支援的間隔常值的逸出序列。 應用程式應該呼叫**SQLGetTypeInfo**來判斷是否支援這些資料類型。
