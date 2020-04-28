---
title: 步驟1：連接到資料來源 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a104733c0e5ec5acc87eeabd00c4e51d4bfd000
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301348"
---
# <a name="step-1-connect-to-the-data-source"></a>步驟 1：連線到資料來源
任何應用程式的第一個步驟是連接到資料來源。 下圖顯示此階段，包括其所需的功能。  
  
 ![連接至 ODBC 應用程式中的資料來源](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 連接到資料來源的第一個步驟是載入驅動程式管理員，並使用**SQLAllocHandle**配置環境控制碼。 如需詳細資訊，請參閱配置[環境控制碼](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 然後，應用程式會使用 SQL_ATTR_APP_ODBC_VER 環境屬性呼叫**SQLSetEnvAttr** ，以註冊它所符合的 ODBC 版本。 如需詳細資訊，請參閱宣告[應用程式的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)和回溯[相容性和標準合規](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)性。  
  
 接下來，應用程式會使用**SQLAllocHandle**配置連接控制碼，並使用**SQLConnect**、 **SQLDriverConnect**或**SQLBrowseConnect**連接至資料來源。 如需詳細資訊，請參閱配置[連接控制碼](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)和[建立連接](../../../odbc/reference/develop-app/establishing-a-connection.md)。  
  
 然後，應用程式會設定任何連接屬性，例如是否手動認可交易。 如需詳細資訊，請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。
