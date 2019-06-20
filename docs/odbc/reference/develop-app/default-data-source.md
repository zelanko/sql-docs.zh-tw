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
manager: craigg
ms.openlocfilehash: 909f9b3e7c8087add8eb66ca2f5c15253026304c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267660"
---
# <a name="default-data-source"></a>預設資料來源
驅動程式可能會選取資料來源，呼叫預設的資料來源，在某些情況下，應用程式並未明確指定其中一個：  
  
-   在呼叫**SQLConnect**何處*ServerName*引數是長度為零的字串、 null 指標或預設值。  
  
-   在呼叫**SQLDriverConnect**其中*InConnectionString*其中一個指定**DSN**= 預設值或指定具有**DSN**關鍵字未包含在系統資訊的資料來源。  
  
 它是驅動程式定義的指定預設的資料來源的方式。 這可能牽涉到系統管理動作，並可能相依於使用者。
