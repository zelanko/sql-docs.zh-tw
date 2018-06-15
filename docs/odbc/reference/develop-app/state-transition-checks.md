---
title: 狀態轉換檢查 |Microsoft 文件
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
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23f2b87fc943535075e1456bb31366ff9667b07b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910623"
---
# <a name="state-transition-checks"></a>檢查狀態轉換
驅動程式管理員會檢查環境、 連線或陳述式的狀態是適用於所呼叫的函式。 比方說，連線必須在配置狀態**SQLConnect**呼叫; 陳述式必須在備妥狀態**SQLExecute**呼叫。 驅動程式管理員狀態轉換錯誤會傳回 SQL_ERROR。
