---
title: 以檔案為基礎的驅動程式診斷的範例 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d58072bebac57eca8976064b85a25999475a9586
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="file-based-driver-diagnostic-example"></a>以檔案為基礎的驅動程式診斷的範例
以檔案為基礎的驅動程式可同時作為 ODBC 驅動程式和資料來源。 它可因此產生錯誤和警告同時做為元件中的 ODBC 連接，並做為資料來源。 它也是介面的驅動程式管理員元件，因為格式化，並傳回引數**SQLGetDiagRec**。  
  
 例如，如果 dBASE Microsoft® 驅動程式無法配置足夠的記憶體，它可能會傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 因為這個錯誤與資料來源已不相關，此驅動程式只加入前置詞診斷訊息 ([Microsoft]) 的廠商和驅動程式 ([ODBC dBASE 驅動程式])。  
  
 如果驅動程式找不到檔案 Employee.dbf，它可能會傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 因為這個錯誤與資料來源相關聯，驅動程式加入資料來源 ([dBASE]) 的檔案格式做為前置詞診斷訊息。 由於驅動程式也是 interfaced 與資料來源的元件，它會加入前置詞 ([Microsoft]) 的廠商和驅動程式 ([ODBC dBASE 驅動程式])。
