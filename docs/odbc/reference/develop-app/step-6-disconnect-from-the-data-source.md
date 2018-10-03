---
title: 步驟 6： 中斷與資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a42465e763f8f6d520ed9c1dac42612aa1b28575
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47802436"
---
# <a name="step-6-disconnect-from-the-data-source"></a>步驟 6：中斷與資料來源的連線
最後一個步驟是中斷連接資料來源，如下圖所示。 首先，應用程式，以釋放任何陳述式控制代碼呼叫**SQLFreeHandle**。 如需詳細資訊，請參閱 <<c0> [ 釋放陳述式控制代碼](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 ![顯示從資料來源中斷連接](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 接下來，應用程式中斷連接與資料來源**SQLDisconnect**並釋放連接控制代碼**SQLFreeHandle**。 如需詳細資訊，請參閱 <<c0> [ 從資料來源或驅動程式中斷連接](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
 最後，應用程式會釋放環境控制代碼**SQLFreeHandle**載入和卸載驅動程式管理員。 如需詳細資訊，請參閱 <<c0> [ 配置環境處理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。
