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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 978362b7dfe92d1333f83be684f6326cf25dd69b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305989"
---
# <a name="default-data-source"></a>預設資料來源
在某些情況下，如果應用程式未明確指定，驅動程式可能會選取一個資料來源，稱為預設資料來源：  
  
-   在**SQLConnect**的呼叫中， *ServerName*引數是長度為零的字串、Null 指標或預設值。  
  
-   在呼叫**SQLDriverConnect** ，其中*InConnectionString*會指定**dsn**= DEFAULT，或使用**dsn**關鍵字指定不包含在系統資訊中的資料來源。  
  
 它是由驅動程式定義的預設資料來源的指定方式。 這可能牽涉到系統管理動作，而且可能會因使用者而異。
