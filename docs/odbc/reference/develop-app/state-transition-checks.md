---
title: 狀態轉換檢查 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dcfefffb167b97ace09bfa358296d886265a987f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809626"
---
# <a name="state-transition-checks"></a>狀態轉換檢查
驅動程式管理員會檢查環境、 連線或陳述式的狀態適用於所呼叫的函式。 比方說，連線必須在配置時**SQLConnect**稱為; 陳述式必須在備妥時狀態**SQLExecute**呼叫。 驅動程式管理員會傳回 SQL_ERROR 狀態轉換錯誤。
