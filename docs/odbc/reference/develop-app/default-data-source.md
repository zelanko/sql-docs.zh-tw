---
title: 預設資料來源 :微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 978362b7dfe92d1333f83be684f6326cf25dd69b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305989"
---
# <a name="default-data-source"></a>預設資料來源
在某些情況下,驅動程式未顯式指定一個資料來源,稱為預設資料來源:  
  
-   在呼叫**SQLConnect**時,*伺服器名稱*參數是零長度字串、空指標或 DEFAULT。  
  
-   在**SQLDriverConnect**的呼叫中 *,其中 InConnectionString*指定**DSN**_DEFAULT,或者使用**DSN**關鍵字指定系統資訊中未包含的資料來源。  
  
 它是驅動程式定義的指定預設數據來源的方式。 這可能涉及管理操作,並且可能取決於使用者。
