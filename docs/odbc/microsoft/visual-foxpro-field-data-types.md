---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 217058bf328677bf375d346ae7201c6eb81efa4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087945"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 欄位資料類型
下表列出 ALTER TABLE 和 CREATE TABLE 中*FieldType*引數的值，並指出是否需要*nFieldWidth*和*nPrecision*引數。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|描述|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|DOUBLE|  
|C|N|-|寬度*n*的字元欄位|  
|D|-|-|Date|  
|F|N|d|寬度*n*的浮動數值欄位與*d*位小數位數|  
|G|-|-|一般|  
|I|-|-|整數|  
|L|-|-|邏輯|  
|M|-|-|備忘錄|  
|N|N|d|寬度*n*與*d*位小數位數的數值欄位|  
|T|-|-|Datetime|  
|Y|-|-|貨幣|
