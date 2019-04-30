---
title: 建立資料表陳述式限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5eab1c3bf6891f10c897966035dced2ffdc10ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232214"
---
# <a name="create-table-statement-limitations"></a>CREATE TABLE 陳述式限制
使用 Microsoft Access、 Microsoft Excel 或 Paradoxdriver 時，文字或二進位資料行長度未指定 （或指定為 0），資料行的長度會設定為 255。  
  
 使用 dBASE 驅動程式時，文字或二進位資料行長度未指定 （或指定為 0），資料行長度將會設定為 254。  
  
 支援最多 255 個資料行。  
  
 無法建立 MicrosoftExcel 5.0、 7.0、 或 97 中的資料來源時，工作表上使用 Microsoft Excel 驅動程式時，先前已卸除工作表同名。 存取版本 5.0、 7.0、 或 97 工作表使用 Microsoft Excel 驅動程式時，DROP TABLE 陳述式就會清除工作表中，但不會刪除工作表名稱。  
  
 使用 Paradox 驅動程式時，就無法加入資料行的資料表上定義索引之後。 如果 CREATE TABLE 陳述式的引數清單的第一個資料行建立索引，第二個資料行不能包含引數清單中。
