---
title: SQLGetTypeInfo （文字檔案驅動程式） |Microsoft 文件
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
ms.topic: article
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4b84e9e826eb2ad3104f00d9d39224fb2da6303
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo （文字檔案驅動程式）
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 傳回所產生之資料表中的型別 (TYPE_NAME) 名稱**SQLGetTypeInfo**會是最常用的資料來源的名稱。  
  
 SQL_ALL_EXCEPT_LIKE 將會傳回可搜尋的資料行中的位元組、 計數器、 Double、 單一、 長時間和 Short 資料類型。 （LIKE 功能可藉由將值轉換成字元，使用 ODBC 標準轉換函式，然後執行比較。）  
  
 使用文字驅動程式時， **SQLGetTypeInfo**資料類型 （CHAR 和 LONGCHAR），傳回文字 CASE_SENSITIVE 值為 FALSE 時的資料型別實際上會區分大小寫。
