---
title: SQLGet資料(桌面資料庫驅動程式) |微軟文件
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
ms.openlocfilehash: 2b102d8435831d45aad3c2049581513e0493de9a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304119"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (桌面資料庫驅動程式)
此函數可以從任何列檢索數據,無論列之後是否有綁定列,也不管檢索列的順序如何。  
  
> [!NOTE]  
>  \*在 Jet 4.0 資料庫中綁定到 ANSI 資料時 **,SQLGetData**中的 pcbValue 返回的字元數可能是實際可用的字元數的兩倍。 510 或更少的字元值將返回實際 cbValue。
