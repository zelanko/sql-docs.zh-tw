---
description: 測試可互通的應用程式
title: 測試互通的應用程式 |Microsoft Docs
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
ms.openlocfilehash: feebbe5914e9da1e414f5c77a1a69bc0a6e0e7b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487521"
---
# <a name="testing-interoperable-applications"></a>測試可互通的應用程式
測試互通的應用程式最棒的一點是，因為新的驅動程式會持續出現在市場上，所以最糟的商務也不可能發生。 不過，可能會有合理程度的測試。 具有有限或低互通性的應用程式只需要針對它們保證支援的驅動程式進行測試。 不過，它們必須針對這些驅動程式進行完整測試。  
  
 可高度互通的應用程式無法實際針對所有驅動程式進行測試。 大部分的應用程式開發人員所能做的，就是完全針對少數驅動程式進行測試，並 cursorily 其他幾個驅動程式。 測試的驅動程式應該包含應用程式市場中最受歡迎的 Dbms 最受歡迎的驅動程式;如果市場涵蓋所有 Dbms，則應該測試桌上型電腦和伺服器 Dbms 的驅動程式。  
  
 測試 ODBC 應用程式的其中一個問題是涉及的元件數目：應用程式本身、驅動程式管理員、驅動程式、DBMS，以及可能的網路軟體或閘道。 應用程式可透過 **SQLGetDiagField** 和 **SQLGetDiagRec**張貼 ODBC 函數所傳回的錯誤訊息，讓您更輕鬆地追蹤錯誤。 這些訊息會識別發生錯誤的製造商和元件。 如需詳細資訊，請參閱 [診斷](../../../odbc/reference/develop-app/diagnostics.md)。
