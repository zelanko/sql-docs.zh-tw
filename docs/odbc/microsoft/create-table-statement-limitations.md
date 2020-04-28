---
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
ms.openlocfilehash: a83acb061cf8192dff1c6adede349f49a0b0bbdb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280869"
---
# <a name="create-table-statement-limitations"></a>CREATE TABLE 陳述式限制
當使用 Microsoft Access、Microsoft Excel 或 Paradoxdriver 時，如果未指定 text 或 binary 資料行的長度（或指定為0），則資料行長度將會設定為255。  
  
 當使用 dBASE 驅動程式，而且未指定 text 或 binary 資料行的長度（或指定為0）時，資料行長度將會設定為254。  
  
 最多支援255個數據行。  
  
 當 Microsoft Excel 驅動程式在 MicrosoftExcel 5.0、7.0 或97資料來源上使用時，無法使用與先前卸載的工作表相同的名稱來建立工作表。 當 Microsoft Excel 驅動程式用來存取5.0、7.0 或97版工作表時，DROP TABLE 語句會清除工作表，但不會刪除工作表名稱。  
  
 當使用 Paradox 驅動程式時，一旦在資料表上定義索引之後，就無法加入資料行。 如果 CREATE TABLE 語句之引數清單的第一個資料行建立索引，第二個數據行就不能包含在引數清單中。
