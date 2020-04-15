---
title: SQLSTATE 映射 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec58c0e41869529bbba5fd31ad534976923a990d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299738"
---
# <a name="sqlstate-mappings"></a>SQLSTATE 對應
本主題討論 ODBC *2.x*和 ODBC *3.x*的 SQLSTATE 值。 有關 ODBC *3.x* SQLSTATE 值的詳細資訊,請參閱[附錄 A:ODBC 錯誤代碼](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。  
  
 在 ODBC *3.x*中,將返回 HYxxx SQLSTATEs 而不是 S1xxx,傳回 42Sxx SQLSTATEs 而不是 S00XX。 這樣做是為了符合開放集團和 ISO 標準。 在許多情況下,映射不是一對一的,因為標準重新定義了對多個 SQLSTAT 的解釋。  
  
 當 ODBC *2.x*應用程式升級到 ODBC *3.x*應用程式時,必須更改應用程式以預期 ODBC *3.x* SQLSTATEs 而不是 ODBC *2.x* SQLSTAT。 下表列出了每個 ODBC *2.x* SQLSTATE 映射到的 ODBC *3.x* SQLSTATEs。  
  
 當SQL_ATTR_ODBC_VERSION環境屬性設置為SQL_OV_ODBC2時,當調用**SQLGetDiagField**或**SQLGetDiagRec**時,驅動程式將發佈 ODBC *2.x* SQLSTATEs 而不是 ODBC *3.x* SQLSTATEs。 可以通過記錄下表第 1 列中對應於第 2 列中的 ODBC *3.x* SQLSTATE 的 ODBC *2.x* SQLSTATE 來確定特定的映射。  
  
|ODBC *2.x* SQLSTATE|ODBC *3.x* SQLSTATE|註解|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24000|07005||  
|37000|42000||  
|70100|HY018||  
|S0001|42S01||  
|S0002|42S02||  
|S0011|42S11||  
|S0012|42S12||  
|S0021|42S21||  
|S0022|42S22||  
|S0023|42S23||  
|S1000|HY000||  
|S1001|HY001||  
|S1002|07009|如果基礎函數是**SQLBindCol、SQLCol****屬性****、SQL 擴展獲取****、SQLFetch、SQLFetchScroll**或**SQLGetData,** 則 ODBC *2.x* SQLSTATE S1002 映射到 ODBC *3.x* SQLSTATE 07009。 **SQLFetchScroll**|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|返回以無效使用空指標。|  
|S1009|HY024|為無效的屬性值返回。|  
|S1009|HY092|傳回以更新或刪除資料,透過呼叫**SQLSetPos**, 或透過呼叫**SQLBulk 操作**(當併發是唯讀的)添加、更新或刪除資料。|  
|S1010|HY007 HY010|SQLSTATE S1010 映射到 SQLSTATE HY007,當**SQLDescribeCol**在呼叫**SQLPrepare、SQLExecDirect**或*語句句柄***SQLExecDirect**的目錄函數之前調用時。 否則,SQLSTATE S1010 將映射到 SQLSTATE HY010。|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|如果基礎函數是**SQLBind 參數**或**SQLDescribeParam,** 則 ODBC *3.x* SQLSTATE 07009 映射到 ODBC *2.x* SQLSTATE S1093。|  
|S1096|HY096||  
|S1097|HY097||  
|S1098|HY098||  
|S1099|HY099||  
|S1100|HY100||  
|S1101|HY101||  
|S1103|HY103||  
|S1104|HY104||  
|S1105|HY105||  
|S1106|HY106||  
|S1107|HY107||  
|S1108|HY108||  
|S1109|HY109||  
|S1110|HY110||  
|S1111|HY111||  
|S1C00|HYC00||  
|S1T00|HYT00||  
  
> [!NOTE]  
>  ODBC *3.x* SQLSTATE 07008 映射到 ODBC *2.x* SQLSTATE S1000。
