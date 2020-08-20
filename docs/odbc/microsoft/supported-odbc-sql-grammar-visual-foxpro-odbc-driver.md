---
description: 支援的 ODBC SQL 文法 (Visual FoxPro ODBC Driver)
title: 支援的 ODBC SQL 文法 (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- native Visual FoxPro language syntax [ODBC]
- FoxPro ODBC driver [ODBC], SQL grammar
- SQL grammar [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], SQL grammar
- grammar support in Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
- FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
ms.assetid: f41a38c2-e22e-4c65-a32e-9a6777435160
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3057520e5aca5277a68971513ef28427f27208ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471500"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>支援的 ODBC SQL 文法 (Visual FoxPro ODBC Driver)
Microsoft Visual FoxPro ODBC 驅動程式支援下列各項：  
  
-   ODBC 最小 SQL 文法中的所有 SQL 語句和子句  
  
-   ODBC core SQL 文法的其他 SQL 語句  
  
 下表列出驅動程式支援的專案（由 ODBC SQL 文法層級所支援）。  
  
|層級|元素|Item|  
|-----------|--------------|----------|  
|最小值|資料定義語言 (DDL)|CREATE TABLE 和 DROP TABLE|  
||資料操作語言 (DML)|SELECT、INSERT、UPDATE 和 DELETE|  
||運算式|簡單 (例如>B + C) |  
||資料類型|CHAR、VARCHAR 或 LONG VARCHAR|  
  
 除了支援的 ODBC SQL 文法之外，Visual FoxPro ODBC 驅動程式還支援下列 Visual FoxPro 命令的完整原生 Visual FoxPro 語言語法：  
  
 [ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [刪除標記](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [指數](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
