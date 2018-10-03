---
title: 步驟 2： 初始化應用程式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0d25173dc8dc14aa1ed41a4a88496ef654e2ff0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850918"
---
# <a name="step-2-initialize-the-application"></a>步驟 2：初始化應用程式
第二步是初始化應用程式，如下圖所示。 完全做些什麼這裡會因為應用程式而有所不同。  
  
 ![顯示 正在初始化 ODBC 應用程式](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 到目前為止，它會使用**SQLGetInfo**探索的驅動程式的功能。 如需詳細資訊，請參閱 <<c0> [ 考慮要使用的資料庫功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)。  
  
 所有應用程式需要配置陳述式控制代碼**SQLAllocHandle**，和許多應用程式設定陳述式屬性，例如資料指標類型、 使用**SQLSetStmtAttr**。 如需詳細資訊，請參閱 <<c0> [ 配置陳述式控制代碼](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)並[陳述式屬性](../../../odbc/reference/develop-app/statement-attributes.md)。
