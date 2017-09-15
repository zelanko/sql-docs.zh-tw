---
title: "呼叫 SQLCloseCursor |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f0d8c7ccb49840ae9477fac5a002b94b79c98302
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="calling-sqlclosecursor"></a>呼叫 SQLCloseCursor
因為**SQLCloseCursor**幾乎相同**SQLFreeStmt** SQL_CLOSE，與驅動程式管理員未對應此函式。 取代函式對應，讓現有的 ODBC 2*.x*應用程式可以輕鬆地將移至 ODBC 3。*x*使用新的函式。 這類移動可讓您更輕鬆地開始使用新的 ODBC 3 這類應用程式。*x*模組化的方式中的條件式程式碼內的功能。 **SQLCloseCursor**不代表任何新功能。 應用程式不會將移至無法取得任何優點**SQLCloseCursor**從**SQLFreeStmt**與 SQL_CLOSE。
