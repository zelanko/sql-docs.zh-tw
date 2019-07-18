---
title: 預設資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to data source [ODBC], default data source
- functions [ODBC], data source or driver connections
- data sources [ODBC], default
- default data source [ODBC]
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], default data source
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: dd473cc6-f051-4aa0-ab14-3dd1b37fe99e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fb016ac7597617b119834e20ffd9e12bd648dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076857"
---
# <a name="default-data-source"></a>預設資料來源
驅動程式可能會選取資料來源，呼叫預設的資料來源，在某些情況下，應用程式並未明確指定其中一個：  
  
-   在呼叫**SQLConnect**何處*ServerName*引數是長度為零的字串、 null 指標或預設值。  
  
-   在呼叫**SQLDriverConnect**其中*InConnectionString*其中一個指定**DSN**= 預設值或指定具有**DSN**關鍵字未包含在系統資訊的資料來源。  
  
 它是驅動程式定義的指定預設的資料來源的方式。 這可能牽涉到系統管理動作，並可能相依於使用者。
