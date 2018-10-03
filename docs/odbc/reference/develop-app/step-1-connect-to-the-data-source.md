---
title: 步驟 1： 連接到資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 154fdd7368835ba2a578d3ec641705c4064859ac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600896"
---
# <a name="step-1-connect-to-the-data-source"></a>步驟 1：連線到資料來源
任何應用程式的第一個步驟是連接到資料來源。 這個階段中，包括它需要，函式會在下圖中顯示。  
  
 ![連接到 ODBC 應用程式中的資料來源](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 連接到資料來源的第一個步驟是載入驅動程式管理員，並配置環境控制代碼**SQLAllocHandle**。 如需詳細資訊，請參閱 <<c0> [ 配置環境處理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 接著，應用程式註冊其符合藉由呼叫的 ODBC 的版本**SQLSetEnvAttr** SQL_ATTR_APP_ODBC_VER 環境屬性。 如需詳細資訊，請參閱 <<c0> [ 宣告應用程式的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)並[回溯相容性與標準相容性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 接下來，應用程式配置連接控制代碼**SQLAllocHandle** ，並連接到資料來源**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**。 如需詳細資訊，請參閱 <<c0> [ 配置連接處理](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)並[建立的連接](../../../odbc/reference/develop-app/establishing-a-connection.md)。  
  
 接著，應用程式設定任何連接屬性，例如是否要以手動方式認可交易。 如需詳細資訊，請參閱 <<c0> [ 連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。
