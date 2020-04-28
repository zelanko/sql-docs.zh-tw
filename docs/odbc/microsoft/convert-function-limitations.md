---
title: 轉換函數限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, CONVERT function limitations
- Convert function limitations [ODBC]
ms.assetid: 3c81fc58-57f0-4dd7-be16-2b146eb15cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63f4258e737327ae11f03a96cfef3cdecf133e53
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281028"
---
# <a name="convert-function-limitations"></a>CONVERT 函式限制
類型轉換失敗會導致受影響的資料行設定為 Null。  
  
 DATE 或 TIMESTAMP 資料類型都不能透過 CONVERT 函數轉換成另一個資料類型（或其本身）。
