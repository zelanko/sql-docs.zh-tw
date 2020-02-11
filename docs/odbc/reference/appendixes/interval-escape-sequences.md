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
ms.openlocfilehash: 69c674ee8838273af9bf4ed91ddcead7e1768fb9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041646"
---
# <a name="interval-escape-sequences"></a>間隔逸出序列
ODBC 會針對間隔常值使用 escape 序列。 此 escape 序列的語法如下：  
  
 {*interval-常*值}  
  
 如需*間隔常*值的 BNF 語法，請參閱本附錄稍後的[間隔常值語法](../../../odbc/reference/appendixes/interval-literal-syntax.md)一節。  
  
 如果資料來源支援間隔資料類型，則支援間隔常值 escape 序列。 應用程式應該呼叫**SQLGetTypeInfo**來判斷是否支援這些資料類型。
