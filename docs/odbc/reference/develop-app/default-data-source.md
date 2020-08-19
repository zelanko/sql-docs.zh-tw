---
description: 預設資料來源
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
ms.openlocfilehash: 0aecd2ec64926a9d1a38d8e3d603124d45223004
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424712"
---
# <a name="default-data-source"></a>預設資料來源
驅動程式可能會在應用程式未明確指定資料來源的情況下，選取稱為預設資料來源的資料來源：  
  
-   在 **SQLConnect** 的呼叫中， *ServerName* 引數為零長度字串、Null 指標或預設值。  
  
-   在呼叫 **SQLDriverConnect** 時， *InConnectionString* 會指定 **dsn**= DEFAULT，或以 **DSN** 關鍵字指定不包含在系統資訊中的資料來源。  
  
 它是驅動程式定義的預設資料來源指定方式。 這可能牽涉到系統管理動作，而且可能依存于使用者。
