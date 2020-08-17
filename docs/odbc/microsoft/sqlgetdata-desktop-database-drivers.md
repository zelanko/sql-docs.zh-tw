---
description: SQLGetData (桌面資料庫驅動程式)
title: SQLGetData (桌面資料庫驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cfce744c3f4a2e0e4d9fcb054a8226538537bdcf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340225"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (桌面資料庫驅動程式)
不論資料行的資料行的取得順序為何，此函數都可以從任何資料行取出資料，而不論資料行是否有系結的資料行。  
  
> [!NOTE]  
>  \*當系結至 Jet 4.0 資料庫上超過510個字元的 ANSI 資料時， **SQLGetData** 中的 pcbValue 可能會傳回兩倍的字元數。 510或更小的字元值會傳回實際的 cbValue。
