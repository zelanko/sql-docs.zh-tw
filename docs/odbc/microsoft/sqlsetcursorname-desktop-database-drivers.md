---
title: SQLSetCursor 名稱(桌面資料庫驅動程式) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d618a7f845a87394c2fc3c7978a7aef5716e21f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301479"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (桌面資料庫驅動程式)
由於驅動程式不支援由 WHERE CURRENT OF*游標名*語法進行定位更新或刪除,因此支援**SQLSetCursorName,** 但不能用於定位更新。 它只能在啟用遊標庫且應用程式使用**SQLExtendedFetch**時使用。
