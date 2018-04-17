---
title: SQLSetCursorName （桌面資料庫驅動程式） |Microsoft 文件
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
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f68d1503d928ab93b3e7d208141eeb065ae9450e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName （桌面資料庫驅動程式）
因為驅動程式不支援定位的更新或刪除 WHERE CURRENT OF *current*語法， **SQLSetCursorName**支援，但不能用於定位更新。 它可以只用於當資料指標程式庫已啟用，且應用程式使用**SQLExtendedFetch**。
