---
title: "Visual FoxPro 欄位資料型別 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c99a094c690882c6f2877964ae19b335cff1509
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 欄位資料類型
下表列出的值*FieldType* ALTER TABLE 和 CREATE TABLE 中的引數，並指出是否*nFieldWidth*和*nPrecision*引數必要項。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|描述|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|c|N|-|字元欄位的寬度*n*|  
|D|-|-|date|  
|F|N|d|浮點數值欄位的寬度 *n* 與*d*小數位數|  
|G|-|-|一般|  
|I|-|-|Integer|  
|L|-|-|邏輯|  
|M|-|-|備忘錄|  
|N|N|d|數值欄位的寬度 *n* 與*d*小數位數|  
|T|-|-|DateTime|  
|Y|-|-|CURRENCY|
