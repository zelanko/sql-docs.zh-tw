---
title: "SQLSetConnectOption （Visual FoxPro ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 14e3708e58d87a1ab38f4b22e9917320969c105b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 部分  
  
 ODBC 應用程式開發介面相容性： 層級 1  
  
 設定選項，以管理連線的層面。 此函式僅部分支援： 此驅動程式支援的所有值*fOption*引數，但不支援某些*vParam*值*fOption*引數SQL_TXN_ISOLATION。  
  
 下表描述這些 Visual FoxPro ODBC 驅動程式實作的特定行為與引數**SQLSetConnectOption**。  
  
|*fOption*|備註|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|如果您選擇 SQL_AUTOCOMMIT_OFF 時，您的應用程式必須明確地認可或回復與交易[SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); Visual FoxPro ODBC 驅動程式不會自動認可可交易的陳述式完成時。 如果可交易的陳述式，此驅動程式並開始交易。|  
|SQL_CURRENT_QUALIFIER|可以是完整[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)名稱或完整的路徑到目錄，包含零或多個[釋放資料表](../../odbc/microsoft/visual-foxpro-terminology.md)。|  
|SQL_LOGINTIMEOUT|會傳回 「 驅動程式不支援 」 錯誤。|  
|SQL_CURSORS|會傳回 「 驅動程式不支援 」 錯誤。|  
|SQL_PACKET_SIZE|會傳回 「 驅動程式不支援 」 錯誤。|  
|SQL_TXN_ISOLATION|驅動程式可讓您僅 SQL_TXN_READ_COMMITTED。<br /><br /> 下列*vParam*s 不支援：<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE 的情況下|  
  
 如需詳細資訊，請參閱[SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md)中*ODBC 程式設計人員參考*。

