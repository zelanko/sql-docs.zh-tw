---
title: SQLGetData （桌面資料庫驅動程式） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f362d725f8b734ab9ecdbdc79c268af08a495b4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313135"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (桌面資料庫驅動程式)
此函式可以從任何資料行，擷取資料，不論是否有繫結資料行之後，也不論在其中擷取資料行的順序。  
  
> [!NOTE]  
>  \*在 pcbValue **SQLGetData**可能會傳回兩倍做為實際可用的字元長度超過在 Jet 4.0 資料庫 510 個字元的 ANSI 資料繫結時。 510 個或更少的字元值會傳回實際 cbValue。
