---
title: SQLSetConnectOption (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 398d098615a0453cb016286867836388fd817540
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473029"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：Partial  
  
 ODBC API 相容性：層級 1  
  
 設定管理許多層面的連線的選項。 此函式僅部分支援：此驅動程式支援的所有值*fOption*引數，但不支援部分*vParam*值*fOption* SQL_TXN_ISOLATION 的引數。  
  
 下表描述這些 Visual FoxPro ODBC Driver 實作特有的行為與引數**SQLSetConnectOption**。  
  
|*fOption*|備註|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|如果您選擇 SQL_AUTOCOMMIT_OFF 時，您的應用程式必須明確地認可或回復交易[SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); Visual FoxPro ODBC 驅動程式不會自動認可可交易的陳述式完成時。 如果可交易的陳述式，驅動程式並開始交易。|  
|SQL_CURRENT_QUALIFIER|可以是完整限定[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)名稱或完整的路徑的目錄，包含零個或多個[免費資料表](../../odbc/microsoft/visual-foxpro-terminology.md)。|  
|SQL_LOGINTIMEOUT|會傳回 「 不支援驅動程式 」 錯誤。|  
|SQL_CURSORS|會傳回 「 不支援驅動程式 」 錯誤。|  
|SQL_PACKET_SIZE|會傳回 「 不支援驅動程式 」 錯誤。|  
|SQL_TXN_ISOLATION|驅動程式可讓只 SQL_TXN_READ_COMMITTED。<br /><br /> 下列*vParam*s 不支援：<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 如需詳細資訊，請參閱 < [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md)中*ODBC 程式設計人員參考*。
