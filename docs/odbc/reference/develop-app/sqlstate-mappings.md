---
description: SQLSTATE 對應
title: SQLSTATE 對應 |Microsoft Docs
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
ms.openlocfilehash: 14be1946b34433b0ff094cb79e2a1ec2ee849cd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476400"
---
# <a name="sqlstate-mappings"></a>SQLSTATE 對應
本主題討論 ODBC *2.x 和 odbc* *3.x 的 SQLSTATE 值。* 如需 ODBC *3.X SQLSTATE 值* 的詳細資訊，請參閱 [附錄 A： odbc 錯誤碼](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。  
  
 在 ODBC *3.x 中，* 會傳回 HYxxx SQLSTATEs 而不是 S1xxx，並傳回 42Sxx SQLSTATEs 而不是 S00XX。 這是為了配合開放式群組和 ISO 標準而完成。 在許多情況下，因為這些標準已重新定義了數個 SQLSTATEs 的轉譯，所以不是一對一的對應。  
  
 當 ODBC 2.x*應用程式升級為 odbc* *3.x 應用程式*時，應用程式必須變更為預期 odbc 3.x SQLSTATEs，而不是*odbc 2.x* *SQLSTATEs。* 下表列出每個 ODBC 2.x *SQLSTATE 對應的 odbc* *3.x SQLSTATEs。*  
  
 當 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC2 時，驅動程式會在呼叫**SQLGetDiagField**或**SQLGetDiagRec**時，張貼 odbc 2.x SQLSTATEs，而不*是 odbc 3.x* *SQLSTATEs。* 您可以在下表的第1欄中，記下對應到資料行2中 ODBC *3.X SQLSTATE 的 odbc* *2.x SQLSTATE，* 來判斷特定的對應。  
  
|ODBC *2.X* SQLSTATE|ODBC *3.X* SQLSTATE|註解|  
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
|S1002|07009|如果基礎函數是**SQLBindCol**、 **SQLColAttribute**、 **SQLExtendedFetch**、 **SQLFetch**、 **SQLFetchScroll**或**SQLGetData**，odbc *2.x SQLSTATE S1002*就會對應到 odbc 3.x *SQLSTATE 07009* 。|  
|S1003|HY003 以及||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|傳回 null 指標的無效用法。|  
|S1009|HY024|傳回不正確屬性值。|  
|S1009|HY092|傳回以透過呼叫 **SQLSetPos**來更新或刪除資料，或在並行處理為唯讀時，藉由呼叫 **SQLBulkOperations**來新增、更新或刪除資料。|  
|S1010|HY007 HY010|SQLSTATE S1010 會在呼叫 SQLDescribeCol、 **SQLPrepare**或*SQLExecDirect*的目錄函數之前**呼叫** **StatementHandle**時，對應到 SQLSTATE HY007。 否則，SQLSTATE S1010 會對應到 SQLSTATE HY010。|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|如果基礎函數是**SQLBindParameter**或**SQLDescribeParam**，odbc 3.x SQLSTATE 07009 會對應*到 odbc 2.x* *SQLSTATE S1093* 。|  
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
>  ODBC *3.X SQLSTATE 07008* 會對應到 odbc 2.X SQLSTATE *S1000* 。
