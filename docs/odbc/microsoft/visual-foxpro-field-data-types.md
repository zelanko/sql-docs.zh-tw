---
description: Visual FoxPro 欄位資料類型
title: Visual FoxPro 欄位資料類型 |Microsoft Docs
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
ms.openlocfilehash: 65410f16367af8764e8572c58e53831f3f7b9cda
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449050"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 欄位資料類型
下表列出 ALTER TABLE 和 CREATE TABLE 中 *FieldType* 引數的值，並指出是否需要 *nFieldWidth* 和 *nPrecision* 引數。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|描述|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|寬度*n*的字元欄位|  
|D|-|-|Date|  
|F|N|d|寬度 *n* 的浮動數值欄位與 *d* 位數|  
|G|-|-|一般|  
|I|-|-|整數|  
|L|-|-|邏輯|  
|M|-|-|備忘錄|  
|N|N|d|具有*d*位小數位數的寬度*n*的數值欄位|  
|T|-|-|Datetime|  
|Y|-|-|貨幣|
