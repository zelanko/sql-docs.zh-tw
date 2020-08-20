---
description: 追蹤
title: 追蹤 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], about tracing
- driver manager [ODBC], tracing
ms.assetid: 77ed4c6c-d976-4eb2-8526-a12697b0ef83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25a7a08fb5c5d2fb203151fb014bdc0edfd25746
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487481"
---
# <a name="tracing"></a>追蹤
ODBC 驅動程式管理員有一個追蹤設備，可讓 ODBC 應用程式所進行的函式呼叫順序記錄並轉譯到記錄檔中。 追蹤是由追蹤 DLL 執行，此 DLL 會在應用程式與驅動程式管理員之間，以及在驅動程式管理員與驅動程式之間，捕獲呼叫。 這種追蹤方法*會以 Odbc* Spy 取代 odbc*2.X 驅動程式*管理員所執行的追蹤，以及 odbc 2.x 中執行的追蹤。  
  
 此章節包含下列主題。  
  
-   [追蹤 DLL](../../../odbc/reference/develop-app/trace-dll.md)  
  
-   [追蹤檔案](../../../odbc/reference/develop-app/trace-file.md)  
  
-   [啟用追蹤](../../../odbc/reference/develop-app/enabling-tracing.md)  
  
-   [動態追蹤](../../../odbc/reference/develop-app/dynamic-tracing.md)
