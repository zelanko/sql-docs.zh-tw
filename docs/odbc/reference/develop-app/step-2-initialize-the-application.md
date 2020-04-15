---
title: 第 2 步:初始化應用程式 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288264"
---
# <a name="step-2-initialize-the-application"></a>步驟 2：初始化應用程式
第二步是初始化應用程式,如下圖所示。 此處完成的確切內容隨應用程式而異。  
  
 ![顯示 ODBC 應用程式的初始化](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 此時,通常使用**SQLGetInfo**來發現驅動程式的功能。 有關詳細資訊,請參閱[考慮使用資料庫功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)。  
  
 所有應用程式都需要使用**SQLAllocHandle**分配敘述,許多應用程式使用**SQLSetStmtAttr**設定語句屬性(如游標類型)。 有關詳細資訊,請參閱[分配敘述的句柄](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)與[語句屬性](../../../odbc/reference/develop-app/statement-attributes.md)。
