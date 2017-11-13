---
title: "Visual FoxPro 欄位資料型別 |Microsoft 文件"
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
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c1ae849d91962cb7d11ca8bac755665217fe1a2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 欄位資料類型
下表列出的值*FieldType* ALTER TABLE 和 CREATE TABLE 中的引數，並指出是否*nFieldWidth*和*nPrecision*引數必要項。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|字元欄位的寬度*n*|  
|D|-|-|日期|  
|F|N|d|浮點數值欄位的寬度 *n* 與*d*小數位數|  
|G|-|-|一般|  
|I|-|-|Integer|  
|L|-|-|邏輯|  
|M|-|-|備忘錄|  
|N|N|d|數值欄位的寬度 *n* 與*d*小數位數|  
|T|-|-|DateTime|  
|Y|-|-|貨幣|

