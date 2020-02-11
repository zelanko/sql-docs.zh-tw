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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65cc8fa7517d3093b7314cacdafd8f607d89bc3a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081989"
---
# <a name="convert-function-limitations"></a>CONVERT 函式限制
類型轉換失敗會導致受影響的資料行設定為 Null。  
  
 DATE 或 TIMESTAMP 資料類型都不能透過 CONVERT 函數轉換成另一個資料類型（或其本身）。
