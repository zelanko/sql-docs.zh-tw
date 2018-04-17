---
title: 步驟 1： 連接到資料來源 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8774e88d3a0301abb3af79b2983870215583532f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="step-1-connect-to-the-data-source"></a>步驟 1： 連接到資料來源
在任何應用程式中的第一個步驟是連接到資料來源。 這個階段中，包括它需要時，函式會在下圖顯示。  
  
 ![連接到資料來源的 ODBC 應用程式中](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 連接到資料來源的第一個步驟是載入驅動程式管理員，並配置環境控制代碼與**SQLAllocHandle**。 如需詳細資訊，請參閱[配置環境處理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 接著，應用程式註冊它符合呼叫的 ODBC 版本**SQLSetEnvAttr** SQL_ATTR_APP_ODBC_VER 環境屬性。 如需詳細資訊，請參閱[宣告應用程式的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)和[回溯相容性和標準相容性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 接下來，應用程式配置連接控制代碼與**SQLAllocHandle**並連接到資料來源與**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**。 如需詳細資訊，請參閱[配置連接處理](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)和[建立連線](../../../odbc/reference/develop-app/establishing-a-connection.md)。  
  
 接著，應用程式設定任何連接屬性，例如是否要以手動方式認可的交易。 如需詳細資訊，請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。
