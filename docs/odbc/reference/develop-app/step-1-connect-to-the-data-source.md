---
title: 第 1 步:連線到資料來源 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301348"
---
# <a name="step-1-connect-to-the-data-source"></a>步驟 1：連線到資料來源
任何應用程式的第一步是連接到數據源。 此階段(包括所需的功能)如下圖所示。  
  
 ![連接至 ODBC 應用程式中的資料來源](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 連接到資料源的第一步是載入驅動程式管理員,並使用**SQLAllocHandle**分配環境句柄。 有關詳細資訊,請參閱[分配環境句柄](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 然後,應用程式通過將**SQLSetEnvAttr**與SQL_ATTR_APP_ODBC_VER環境屬性調用,註冊其符合的 ODBC 版本。 有關詳細資訊,請參閱[宣告應用程式的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)和[向後相容性和標準合規性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 接下來,應用程式使用**SQLAllocHandle**分配連接句柄,並透過**SQLConnect、SQLDriverConnect**或**SQLDriverConnect** **SQLBrowseConnect**連接到數據源。 有關詳細資訊,請參閱[分配連接句柄](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)與[建立連線](../../../odbc/reference/develop-app/establishing-a-connection.md)。  
  
 然後,應用程式設置任何連接屬性,例如是否手動提交事務。 有關詳細資訊,請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。
