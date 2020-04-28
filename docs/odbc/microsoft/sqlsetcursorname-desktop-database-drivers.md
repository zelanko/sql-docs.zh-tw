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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d618a7f845a87394c2fc3c7978a7aef5716e21f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301479"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (桌面資料庫驅動程式)
因為驅動程式不支援定點更新或刪除，其中目前的*cursorname*語法，所以支援**SQLSetCursorName** ，但不能用於定點更新。 只有在已啟用資料指標程式庫，且應用程式使用**SQLExtendedFetch**時，才可以使用它。
