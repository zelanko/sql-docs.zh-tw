---
title: SQLSetCursorName （桌面資料庫驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e433e6aee341085965f361992fc8ea9ac8744353
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305625"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (桌面資料庫驅動程式)
因為此驅動程式不支援定位的更新或刪除 WHERE CURRENT OF *current*語法**SQLSetCursorName**支援，但不能用於定位更新。 它僅適用於當資料指標程式庫已啟用，而且應用程式使用**SQLExtendedFetch**。
