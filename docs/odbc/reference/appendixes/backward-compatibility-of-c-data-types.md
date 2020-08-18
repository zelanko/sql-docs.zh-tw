---
description: C 資料類型的回溯相容性
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e50a07d3c49438fcdfbc0b57ec70380d20c88440
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411314"
---
# <a name="backward-compatibility-of-c-data-types"></a>C 資料類型的回溯相容性
在 ODBC 中，SQL_C_SHORT、SQL_C_LONG 和 SQL_C_TINYINT 已經過正負號和不帶正負號的類型取代： SQL_C_SSHORT 和 SQL_C_USHORT、SQL_C_SLONG 和 SQL_C_ULONG，以及 SQL_C_STINYINT 和 SQL_C_UTINYINT。 應該搭配 *odbc 2.x* 應用程式使用的 odbc 3.x 驅動程式應該支援 SQL_C_SHORT、SQL_C_LONG 和 SQL_C_TINYINT，因為當呼叫它們時， *驅動程式管理員* 會將它們傳遞到驅動程式。
