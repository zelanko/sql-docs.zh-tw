---
title: "預設資料來源 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 08c8aab7a9cfcecf18181dacbab6f18aaa59ff64
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="default-data-source"></a>預設的資料來源
驅動程式可能會選取資料來源，呼叫預設的資料來源，在某些情況下，應用程式並未明確指定其中一個：  
  
-   在呼叫**SQLConnect**其中*ServerName*引數是零長度字串、 null 指標或 DEFAULT。  
  
-   在呼叫**SQLDriverConnect**其中*InConnectionString*是指定**DSN**= 預設值或指定**DSN**關鍵字並未包含在系統資訊的資料來源。  
  
 它為驅動程式定義的預設資料來源指定的方式。 這可能牽涉到系統管理動作，可能會取決於使用者。

