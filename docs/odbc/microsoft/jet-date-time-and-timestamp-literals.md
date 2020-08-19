---
description: Jet：日期、時間和時間戳記常值
title: Jet：日期、時間和時間戳記常值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02b2a7c5c633ee891dbcd962786cb1904bfd5df8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449440"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet：日期、時間和時間戳記常值
為了達到最大的互通性，應用程式應該使用 escape 子句語法來傳遞 ODBC 標準格式的日期常值：  
  
-   針對日期常值 {d '*value*'}，其中 *宣告*e 的格式為 "yyyy-mm-dd"  
  
-   針對時間常值，{t '*value*'}，其中 *宣告*e 的格式為 "hh： mm： ss"  
  
 針對時間戳記常值 {ts '*value*'}，其中 *宣告*e 的格式為 "yyyy-mm-dd hh： mm： ss [f. ...]"。
