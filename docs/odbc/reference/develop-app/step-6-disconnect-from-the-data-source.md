---
title: '步驟 6: 中斷與資料來源 |Microsoft 文件'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db689d042d4dedd12f487933783ad89018433d69
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915003"
---
# <a name="step-6-disconnect-from-the-data-source"></a>步驟 6： 中斷與資料來源
最後一個步驟是中斷連接資料來源，在下圖所示。 首先，應用程式會釋放任何陳述式控制代碼藉由呼叫**SQLFreeHandle**。 如需詳細資訊，請參閱[釋放陳述式控制代碼](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 ![顯示從資料來源中斷連線](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 接下來，應用程式中斷連接資料來源與**SQLDisconnect**並釋放連接控制代碼與**SQLFreeHandle**。 如需詳細資訊，請參閱[中斷資料來源或驅動程式](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
 最後，應用程式會釋放環境控制代碼與**SQLFreeHandle**載入和卸載驅動程式管理員。 如需詳細資訊，請參閱[配置環境處理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。
