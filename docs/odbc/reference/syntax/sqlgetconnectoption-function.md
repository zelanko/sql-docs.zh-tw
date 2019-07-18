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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103828"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：已被取代  
  
 **摘要**  
 在 ODBC *3.x*，ODBC *2.x*函式**SQLGetConnectOption**已被取代**SQLGetConnectAttr**。 如需詳細資訊，請參閱 < [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)。  
  
> [!NOTE]
>  如需有關什麼驅動程式管理員會對應到此函式時 ODBC *2.x*應用程式使用 ODBC *3.x*驅動程式，請參閱[對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)附錄 g:為了與舊版相容的驅動程式指導方針。  
> 
> [!NOTE]
>  不支援屬性符合 ODBC 3.8 中導入的 SQL_ASYNC_DBC_FUNCTION_ENABLE **SQLGetConnectOption**。 使用連接控制代碼上的非同步作業的應用程式必須使用**SQLGetConnectAttr**。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
