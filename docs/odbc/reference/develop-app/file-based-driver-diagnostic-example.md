---
title: 以檔案的驅動程式診斷範例 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f09e4f4758b6276836b08f02b24fb31dd1fadc7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305636"
---
# <a name="file-based-driver-diagnostic-example"></a>以檔案為基礎的驅動程式診斷範例
基於檔案的驅動程式既充當 ODBC 驅動程式,又充當數據來源。 因此,它可以生成錯誤和警告,同時作為ODBC連接中的元件和數據源生成。 因為它也是與驅動程式管理器介面的元件,因此它格式化並返回**SQLGetDiagRec**的參數。  
  
 例如,如果 dBASE 的 Microsoft ®驅動程式無法分配足夠的記憶體,它可能會從**SQLGetDiarec**傳回以下值 :  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 由於此錯誤與資料源無關,驅動程式僅向供應商 ([Microsoft]) 和驅動程式([ODBC dBASE 驅動程式])的診斷消息添加了首碼。  
  
 如果驅動程式找不到檔案 Employ.dbf,它可能會從**SQLGetDiagRec**傳回以下值 :  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 由於此錯誤與資料源相關,驅動程式添加了數據源 ([dBASE]) 的檔案格式作為診斷消息的首碼。 由於驅動程式也是與數據源介面的元件,因此添加了供應商([微軟])和驅動程式([ODBC dBASE 驅動程式])的首碼。
