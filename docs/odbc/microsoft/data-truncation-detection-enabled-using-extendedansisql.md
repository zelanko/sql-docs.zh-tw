---
title: 啟用使用 ExtendedAnsiSQL 資料截斷偵測 |Microsoft 文件
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
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08183430384a7a5ced14871c7bd151cb21c40b2b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>啟用使用 ExtendedAnsiSQL 資料截斷偵測。
當 ExtendedAnsiSQL 旗標開啟應用程式會將資料插入 char 或 binary 資料行及資料遭到截斷時，就會偵測到截斷。 ExtendedAnsiSQL 旗標為關閉時，會將資料截斷而不發出警告，因為是舊版的 ODBC 桌面資料庫驅動程式。
