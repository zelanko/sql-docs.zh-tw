---
title: SQLSTATE 對應 |Microsoft 文件
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
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 402d5b6c01142334ed38a73b96da9f0eb635f1c3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlstate-mappings"></a>SQLSTATE 對應
本主題會討論 ODBC 2 SQLSTATE 值。*x*和 ODBC 3。*x*。 如需有關 ODBC 3 的詳細資訊。*x* SQLSTATE 值，請參閱[附錄 a: ODBC 錯誤碼](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。  
  
 在 ODBC 3。*x*、 HYxxx Sqlstate 會傳回而不是 S1xxx，和 42Sxx Sqlstate 會傳回而不是 S00XX。 這是為了與 Open Group 和 ISO 標準。 在許多情況下，對應不是一對一因為標準已重新定義的數個 Sqlstate 解譯。  
  
 當 ODBC 2。*x*應用程式會升級到 ODBC 3。*x*應用程式，應用程式必須變更為預期 ODBC 3。*x* Sqlstate 而不是 ODBC 2。*x* Sqlstate。 下表列出 ODBC 3。*x* Sqlstate 的每個 ODBC 2。*x* SQLSTATE 對應至。  
  
 當 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC2 時，驅動程式就會公佈 ODBC 2。*x*而不是 ODBC 3 的 Sqlstate。*x* Sqlstate 時**SQLGetDiagField**或**SQLGetDiagRec**呼叫。 特定對應由注意 ODBC 2*.x*對應至 ODBC 3 的下列資料表的資料行 1 中的 SQLSTATE。*x*資料行 2 中的 SQLSTATE。  
  
|ODBC 2。*x* SQLSTATE|ODBC 3。*x* SQLSTATE|註解|  
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
|就會傳回 S1000|HY000||  
|S1001|HY001||  
|S1002|07009|ODBC 2。*x* SQLSTATE S1002 會對應至 ODBC 3。*x* SQLSTATE 如果基礎函式進行 07009 **SQLBindCol**， **SQLColAttribute**， **SQLExtendedFetch**， **SQLFetch**， **SQLFetchScroll**，或**SQLGetData**。|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|傳回使用無效的 null 指標。|  
|S1009|HY024|傳回無效的屬性值。|  
|S1009|HY092|更新或刪除的資料呼叫所傳回的**SQLSetPos**，或加入、 更新或刪除資料，藉由呼叫**SQLBulkOperations**、 並行唯讀時。|  
|S1010|HY007 HY010|SQLSTATE S1010 會對應至 SQLSTATE HY007 時**SQLDescribeCol**在呼叫之前呼叫**SQLPrepare**， **SQLExecDirect**，或類別目錄函式的*StatementHandle*。 否則，SQLSTATE S1010 會對應至 SQLSTATE HY010。|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC 3。*x* SQLSTATE 07009 會對應至 ODBC 2。*x*如果基礎函式的 SQLSTATE S1093 **SQLBindParameter**或**SQLDescribeParam**。|  
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
>  ODBC 3。*x* SQLSTATE 07008 會對應至 ODBC 2。*x* SQLSTATE S1000。
