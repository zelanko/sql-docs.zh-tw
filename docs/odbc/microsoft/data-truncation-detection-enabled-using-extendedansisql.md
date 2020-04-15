---
title: 使用擴展安西SQL 啟用數據截斷檢測 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae1aa7a8a8b9ea2c3f3054717546506e660d5270
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280693"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>使用 ExtendedAnsiSQL 啟用的資料截斷偵測
當擴展 AnsiSQL 標誌打開,應用程式將數據插入到字元或二進位列中,並且數據被截斷時,將檢測到截斷。 關閉擴展 AnsiSQL 標誌時,數據將被截斷,而不會發出警告,就像以前版本的 ODBC 桌面資料庫驅動程式一樣。
