---
title: "資料型別限制 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 558789a4f435e9fc54176b1423d71369f6b4cc22
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-limitations"></a>資料型別限制
Microsoft ODBC 桌面資料庫驅動程式以強制資料類型的下列限制：  
  
|資料類型|Description|  
|---------------|-----------------|  
|所有資料類型|類型轉換失敗，可能會造成影響的資料行設為 NULL。|  
|BINARY|建立零長度的 BINARY 資料行時，實際上會傳回 255 個位元組的二進位資料行。|  
|DATE|DATE 資料類型無法轉換成另一種資料類型 （或本身），由轉換函式。|  
|DECIMAL （精確數值）|不支援。|  
|浮點資料類型|浮點數中的小數位數可能會受到在 Windows 控制台中的國際區段中設定的數字格式。|  
|NUMERIC|支援最大有效位數和小數位數為 28。|  
|timestamp|TIMESTAMP 資料類型無法轉換成本身的轉換函式。|  
|TINYINT|TINYINT 值一定是不帶正負號。|  
|零長度字串|使用 dBASE、 Microsoft Excel、 Paradox 或 Textdriver 時，將插入的資料行的零長度字串實際插入 null 值改為。|

