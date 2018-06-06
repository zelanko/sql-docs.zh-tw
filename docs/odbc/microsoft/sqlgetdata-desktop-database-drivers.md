---
title: SQLGetData （桌面資料庫驅動程式） |Microsoft 文件
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
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae546182d51663c15a14ac25b5349a06da02e952
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData （桌面資料庫驅動程式）
此函式可以從任何資料行，擷取資料，不論是否有繫結資料行之後，並在其中擷取資料行的順序為何。  
  
> [!NOTE]  
>  \*在 pcbValue **SQLGetData**可能會傳回倍字元為實際可用的繫結至 ANSI 資料超過 Jet 4.0 資料庫超出 510 個字元。 字元值或較少的 510 會傳回實際 cbValue。
