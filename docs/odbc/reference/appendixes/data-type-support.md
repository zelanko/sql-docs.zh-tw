---
title: "資料類型支援 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 147e940dcd37b452e1fe05b3a39f6b184c810397
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-support"></a>資料類型支援
ODBC 驅動程式必須支援至少一個 SQL_CHAR 和 SQL_VARCHAR。 其他資料類型的支援取決於驅動程式或資料來源的 SQL 92 一致性層級。 應用程式應該呼叫**SQLGetTypeInfo**判斷驅動程式所支援的資料類型。  
  
 如需有關資料類型的詳細資訊，請參閱[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。

