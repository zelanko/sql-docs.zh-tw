---
title: 可視化 FoxPro 欄位資料類型 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72313e0269c93bca9cb2561d89604c3c88c8567b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304799"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 欄位資料類型
下表列出了 ALTER TABLE 和 CREATE TABLE 中*欄位類型*參數的值,並指示是否需要*nFieldWidth*和*nPrecision*參數。  
  
|*欄位型別*|*NFieldWidth*|*n精密*|描述|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|*寬度*n 的字元欄位|  
|D|-|-|Date|  
|F|N|d|具有*d*小數字點的寬度*n*的浮動數位欄位|  
|G|-|-|一般|  
|I|-|-|整數|  
|L|-|-|邏輯|  
|M|-|-|備忘錄|  
|N|N|d|帶有*d*小數位的數字寬度*欄位 n*|  
|T|-|-|Datetime|  
|Y|-|-|貨幣|
