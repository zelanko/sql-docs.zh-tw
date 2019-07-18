---
title: 程序呼叫中的參數標記 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bb24fb628e9e49fd94104af05217511a8f57c3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912311"
---
# <a name="parameter-markers-in-procedure-calls"></a>程序呼叫中的參數標記
在呼叫接受參數的程序，可互通的應用程式應該使用參數標記，而不是常值的參數值。 某些資料來源不支援在程序呼叫中使用常值的參數值。 如需有關參數的詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。 如需有關呼叫程序的詳細資訊，請參閱[程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)稍後這一節。
