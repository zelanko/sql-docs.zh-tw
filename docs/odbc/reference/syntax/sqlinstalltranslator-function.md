---
title: "SQLInstallTranslator 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b7efa21691627c346b6d3798ade158e946071e6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函式
**一致性**  
 版本引進了： ODBC 2.5，已被取代  
  
 **摘要**  
 在 ODBC 3.0 **SQLInstallTranslator**已被取代[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。 呼叫**SQLInstallTranslator**將會對應至**SQLInstallTranslatorEx**。 如需詳細資訊，請參閱**SQLInstallTranslatorEx**。  
  
 **SQLInstallTranslator**將傳回 FALSE，如果應用程式會呼叫它在 ODBC 3*.x*驅動程式管理員與*lpszInfFile*引數設定為 NULL 以外的值。 使用 ODBC 2 Odbc.inf 檔案。*x*已不再支援在 ODBC 3*.x*即使回溯相容性。

