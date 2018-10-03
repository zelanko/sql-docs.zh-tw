---
title: SQLRemoveDefaultDataSource 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDefaultDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDefaultDataSource
helpviewer_keywords:
- SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90270f119b351592348287823c2b9d879a15154b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821116"
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource 函式
**合規性**  
 版本導入： ODBC 1.0 時，已被取代  
  
 **摘要**  
 在 ODBC 3.0 **SQLRemoveDefaultDataSource**函式已取代呼叫[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)具有*常見*ODBC_REMOVE_DEFAULT_DSN 引數。 如果 ODBC 2 *.x*安裝程式會呼叫此函式，ODBC 安裝程式會將它對應至下列**SQLConfigDataSource**呼叫：  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
