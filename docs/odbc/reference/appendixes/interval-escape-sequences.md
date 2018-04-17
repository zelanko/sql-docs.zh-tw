---
title: 間隔逸出序列 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a9ef232521850dbf6007942d7758ce2b5820a335
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="interval-escape-sequences"></a>間隔逸出序列
ODBC 使用間隔常值的逸出序列。 此逸出序列語法如下所示：  
  
 {*間隔常值*}  
  
 BNF 語法*間隔常值*，請參閱[間隔常值的語法](../../../odbc/reference/appendixes/interval-literal-syntax.md)稍後在本附錄 > 一節。  
  
 如果資料來源的支援間隔資料類型，支援的間隔常值的逸出序列。 應用程式應該呼叫**SQLGetTypeInfo**以判斷是否支援這些資料類型。
