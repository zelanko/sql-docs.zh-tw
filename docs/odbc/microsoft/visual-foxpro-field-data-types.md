---
title: Visual FoxPro 欄位資料型別 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf6df134c5a4ad54e574e42e57d7a68e10b4e077
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 欄位資料類型
下表列出的值*FieldType* ALTER TABLE 和 CREATE TABLE 中的引數，並指出是否*nFieldWidth*和*nPrecision*引數必要項。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|字元的欄位寬度的*n*|  
|D|-|-|日期|  
|F|N|d|浮點數值欄位的寬度*n*與*d*小數位數|  
|G|-|-|一般|  
|I|-|-|Integer|  
|L|-|-|邏輯|  
|M|-|-|備忘錄|  
|N|N|d|數值欄位的寬度*n*與*d*小數位數|  
|T|-|-|DateTime|  
|Y|-|-|CURRENCY|
