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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905505"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (桌面資料庫驅動程式)
因為驅動程式不支援定點更新或刪除，其中目前的*cursorname*語法，所以支援**SQLSetCursorName** ，但不能用於定點更新。 只有在已啟用資料指標程式庫，且應用程式使用**SQLExtendedFetch**時，才可以使用它。
