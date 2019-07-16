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
ms.openlocfilehash: 53ef01423ad14cb5606e14ca004ca614e68101e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905505"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (桌面資料庫驅動程式)
因為此驅動程式不支援定位的更新或刪除 WHERE CURRENT OF *current*語法**SQLSetCursorName**支援，但不能用於定位更新。 它僅適用於當資料指標程式庫已啟用，而且應用程式使用**SQLExtendedFetch**。
