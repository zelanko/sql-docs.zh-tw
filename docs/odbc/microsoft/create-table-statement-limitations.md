---
description: CREATE TABLE 陳述式限制
title: CREATE TABLE 語句限制 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a903484663eed886f87d983aa027e4cf5b568408
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471620"
---
# <a name="create-table-statement-limitations"></a>CREATE TABLE 陳述式限制
使用 Microsoft Access、Microsoft Excel 或 Paradoxdriver 時，如果未指定文字或二進位資料行的長度 (或指定為 0) ，則資料行長度將會設定為255。  
  
 當使用 dBASE 驅動程式，且未指定 text 或 binary 資料行的長度 (或指定為 0) 時，資料行長度將會設定為254。  
  
 最多可支援255個數據行。  
  
 在 MicrosoftExcel 5.0、7.0 或97資料來源上使用 Microsoft Excel 驅動程式時，無法使用與先前卸載的工作表相同的名稱來建立工作表。 使用 Microsoft Excel 驅動程式存取5.0、7.0 或97版工作表時，DROP TABLE 語句會清除工作表，但不會刪除工作表名稱。  
  
 使用 Paradox 驅動程式時，當資料表上已定義索引時，就無法再加入資料行。 如果 CREATE TABLE 語句的引數清單的第一個資料行建立索引，則第二個數據行不能包含在引數清單中。
