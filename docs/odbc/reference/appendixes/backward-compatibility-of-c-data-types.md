---
title: "回溯相容性的 C 資料類型 |Microsoft 文件"
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
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 24d0c05a7410a3db37718ebaa667abbb01072796
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="backward-compatibility-of-c-data-types"></a>回溯相容性的 C 資料類型
SQL_C_SHORT、 SQL_C_LONG、 和 SQL_C_TINYINT 已取代 ODBC 中的帶正負號和不帶正負號型別： SQL_C_SSHORT 和 SQL_C_USHORT、 SQL_C_SLONG 然後 SQL_C_ULONG、 SQL_C_STINYINT 並 SQL_C_UTINYINT。 ODBC 3*.x*驅動程式可以使用的 ODBC 2。*x*應用程式應該支援 SQL_C_SHORT、 SQL_C_LONG、 和 SQL_C_TINYINT，，因為它們呼叫時，驅動程式管理員將其傳遞到驅動程式。

