---
title: 建立表語句限制 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280869"
---
# <a name="create-table-statement-limitations"></a>CREATE TABLE 陳述式限制
使用 Microsoft Access、Microsoft Excel 或 Paradox 驅動程式,並且未指定文本或二進位列的長度(或指定為 0)時,列長度將設置為 255。  
  
 使用 dBASE 驅動程式且未指定文本或二進位列的長度(或指定為 0)時,列長度將設置為 254。  
  
 最多支援 255 列。  
  
 當在 MicrosoftExcel 5.0、7.0 或 97 資料來源上使用 Microsoft Excel 驅動程式時,無法創建與以前刪除的工作表同名的工作表。 當 Microsoft Excel 驅動程式用於存取版本 5.0、7.0 或 97 工作表時,DROP TABLE 語句將清除工作表,但不會刪除工作表名稱。  
  
 使用 Paradox 驅動程式時,在表上定義索引後無法添加列。 如果 CREATE TABLE 語句的參數清單的第一列建立索引,則第二列不能包含在參數清單中。
