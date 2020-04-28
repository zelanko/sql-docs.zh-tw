---
title: 步驟2：初始化應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 843155ba6b641ea26717e63af55c8774f963a800
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288264"
---
# <a name="step-2-initialize-the-application"></a>步驟 2：初始化應用程式
第二個步驟是初始化應用程式，如下圖所示。 這裡的確切做法會隨著應用程式而有所不同。  
  
 ![顯示 ODBC 應用程式的初始化](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 此時，通常會使用**SQLGetInfo**來探索驅動程式的功能。 如需詳細資訊，請參閱[考慮要使用的資料庫功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)。  
  
 所有應用程式都必須使用**SQLAllocHandle**配置語句控制碼，而許多應用程式會使用**SQLSetStmtAttr**來設定語句屬性（例如資料指標類型）。 如需詳細資訊，請參閱配置[語句控制碼](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)和[語句屬性](../../../odbc/reference/develop-app/statement-attributes.md)。
