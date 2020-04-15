---
title: 測試可相互操作的應用程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1d43c7aad2501591c497475f6c250ac33712aa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307739"
---
# <a name="testing-interoperable-applications"></a>測試可互通的應用程式
測試可互操作的應用程式充其量是一項耗時的業務,在最壞的情況下是不可能的,因為新的驅動程序不斷出現在市場上。 但是,可以進行合理的測試。 互操作性有限或低的應用程式只需根據保證支援的驅動程序進行測試。 但是,必須針對這些驅動程式進行全面測試。  
  
 高度互通的應用程式不能對所有驅動程式進行實際測試。 大多數應用程式開發人員能做的最好的事情就是根據少量驅動程式對其進行完全測試,並粗略地針對多個驅動程式。 經過測試的驅動程式應包括應用程式市場中最流行的 DBMS 的驅動程式;如果市場涵蓋所有 DBMS,則應測試桌上型電腦和伺服器 DBMS 的驅動程式。  
  
 測試 ODBC 應用程式時的問題之一是所涉及的元件數量:應用程式本身、驅動程式管理器、驅動程式、DBMS,以及可能的網路軟體或閘道。 應用程式可以通過**SQLGetDiagField 和 SQLGetDiagRec**發佈**SQLGetDiagRec**ODBC 函數傳回的 錯誤訊息,從而更輕鬆地追蹤錯誤。 這些消息標識發生錯誤的製造商和元件。 有關詳細資訊,請參閱[診斷](../../../odbc/reference/develop-app/diagnostics.md)。
