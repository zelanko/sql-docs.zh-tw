---
title: C 資料類型的向後相容性 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a89b282a2229b6f34833b4371081661ea51b231
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304583"
---
# <a name="backward-compatibility-of-c-data-types"></a>C 資料類型的回溯相容性
SQL_C_SHORT、SQL_C_LONG和SQL_C_TINYINT已在 ODBC 中替換為已簽名和未簽名的類型:SQL_C_SSHORT和SQL_C_USHORT、SQL_C_SLONG和SQL_C_ULONG以及SQL_C_STINYINT和SQL_C_UTINYINT。 應使用 ODBC *2.x*應用程式的 ODBC *3.x*驅動程式應支援SQL_C_SHORT、SQL_C_LONG和SQL_C_TINYINT,因為當調用它們時,驅動程式管理器會將它們傳遞給驅動程式。
