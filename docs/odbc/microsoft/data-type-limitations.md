---
title: 資料類型限制 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4beaf91a4ead743e3e8a2e32578796baba3c17be
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280668"
---
# <a name="data-type-limitations"></a>資料類型限制
Microsoft ODBC 桌面資料庫驅動程式對資料類型施加了以下限制:  
  
|資料類型|描述|  
|---------------|-----------------|  
|所有資料類型|類型轉換失敗可能導致受影響的列設定為 NULL。|  
|BINARY|創建零長度的 BINARY 列實際上返回一個 255 位元組的 BINARY 列。|  
|日期|轉換函數不能將 DATE 資料類型轉換為其他資料類型(或本身)。|  
|DECIMAL(精確數字)|不支援。|  
|浮點資料類型|浮點數位中的小數位數可能受 Windows 控制面板國際部分中設置的數位格式的限制。|  
|NUMERIC|支援最大精度和 28 級。|  
|timestamp|轉換函數不能將時間 STAMP 資料類型轉換為自身。|  
|TINYINT|TINYINT 值始終未簽名。|  
|零長度字串|當使用 dBASE、Microsoft Excel、悖論或文本驅動程式時,將零長度字串插入列實際上插入 NULL。|
