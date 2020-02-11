---
title: SQLGetConnectOption 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7461304a9aa015eac223dc726e669ad5c4ecd4ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103828"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 函式
**標準**  
 引進的版本： ODBC 1.0 標準合規性：已淘汰  
  
 **摘要**  
 在 ODBC 3.x*中，odbc* *2.x 函數* **SQLGetConnectOption**已由**SQLGetConnectAttr**取代。 如需詳細資訊，請參閱[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)。  
  
> [!NOTE]
>  如需 ODBC 2.x 應用程式*使用 odbc 3.x* *驅動程式時*，驅動程式管理員將此函式對應至哪個功能的詳細資訊，請參閱附錄 G：驅動程式方針中的對應已被[取代](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)的函式，以取得回溯相容性。  
> 
> [!NOTE]
>  **SQLGetConnectOption**不支援 ODBC 3.8 中引進的屬性 SQL_ASYNC_DBC_FUNCTION_ENABLE。 在連接控制碼上使用非同步作業的應用程式必須使用**SQLGetConnectAttr**。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
