---
title: 呼叫 SQLGetDiagField |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2ef69704ae6984f41080aea009f17ac09bafefd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134982"
---
# <a name="calling-sqlgetdiagfield"></a>呼叫 SQLGetDiagField
當 ODBC *3.x*應用程式會呼叫**SQLGetDiagField** ODBC 中*2.x*驅動程式，此驅動程式會傳回 SQL_SUCCESS中適當的資訊 *\*DiagInfoPtr*如果*Sqlgetdiagfield*引數是 SQL_DIAG_CLASS_ORIGIN、 SQL_DIAG_CLASS_SUBCLASS_ORIGIN、 SQL_DIAG_CONNECTION_NAME、 SQL_DIAG_MESSAGE_TEXT、 SQL_DIAG_原生 SQL_DIAG_NUMBER、 SQL_DIAG_RETURNCODE、 SQL_DIAG_SERVER_NAME，還是 SQL_DIAG_SQLSTATE。 其他所有的診斷欄位將會傳回 SQL_ERROR。
