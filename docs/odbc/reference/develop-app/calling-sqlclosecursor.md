---
title: 呼叫 SQLCloseCursor |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2feab58de28e39747a1d9c819f9f15426b156151
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306271"
---
# <a name="calling-sqlclosecursor"></a>呼叫 SQLCloseCursor
由於**SQLCloseCursor**與**SQLFreeStmt**與具有SQL_CLOSE幾乎相同,因此驅動程式管理器不會映射此函數。 可映射替換函數,以便現有的 ODBC *2.x*應用程式可以使用新功能輕鬆移動到 ODBC *3.x。* 通過這樣的移動,此類應用程式可以更輕鬆地開始以模組化方式在條件代碼內部使用新的 ODBC *3.x*功能。 **SQLCloseCursor**不表示任何新功能。 應用程式通過使用SQL_CLOSE從**SQLFreeStmt**移動到**SQLCloseCursor**不會獲得任何優勢。
