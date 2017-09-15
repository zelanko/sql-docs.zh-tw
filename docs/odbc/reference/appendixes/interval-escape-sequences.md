---
title: "間隔逸出序列 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8088c0cb3f85b375423f636d2def8c08c04bbe28
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="interval-escape-sequences"></a>間隔逸出序列
ODBC 使用間隔常值的逸出序列。 此逸出序列語法如下所示：  
  
 {*間隔常值*}  
  
 BNF 語法*間隔常值*，請參閱[間隔常值的語法](../../../odbc/reference/appendixes/interval-literal-syntax.md)稍後在本附錄 > 一節。  
  
 如果資料來源的支援間隔資料類型，支援的間隔常值的逸出序列。 應用程式應該呼叫**SQLGetTypeInfo**以判斷是否支援這些資料類型。
