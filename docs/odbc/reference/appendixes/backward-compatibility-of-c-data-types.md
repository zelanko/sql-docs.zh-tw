---
title: C 資料類型的回溯相容性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dcfc4dd2ef1bee2783f073fbb85c0d911f84305a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037798"
---
# <a name="backward-compatibility-of-c-data-types"></a>C 資料類型的回溯相容性
在 ODBC 中，已簽署和不帶正負號的類型已取代 SQL_C_SHORT、SQL_C_LONG 和 SQL_C_TINYINT： SQL_C_SSHORT 和 SQL_C_USHORT、SQL_C_SLONG 和 SQL_C_ULONG，以及 SQL_C_STINYINT 和 SQL_C_UTINYINT。 應該與 ODBC *2.x 應用程式*搭配使用的 odbc *3. x*驅動程式應該支援 SQL_C_SHORT、SQL_C_LONG 和 SQL_C_TINYINT，因為當呼叫它們時，驅動程式管理員會將它們傳遞至驅動程式。
