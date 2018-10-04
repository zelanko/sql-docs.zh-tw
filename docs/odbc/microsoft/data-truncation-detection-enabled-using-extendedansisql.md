---
title: 使用 ExtendedAnsiSQL 啟用的資料截斷偵測 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95b7d538c2ace45b42c947b56ca5a5bd5f981ec5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793646"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>使用 ExtendedAnsiSQL 啟用的資料截斷偵測
當 ExtendedAnsiSQL 旗標開啟應用程式會將資料插入 char 或 binary 資料行且資料會被截斷時，就會偵測到截斷。 ExtendedAnsiSQL 旗標為關閉時，會將資料截斷而不發出警告，因為它是在舊版的 ODBC 桌面資料庫驅動程式。
