---
title: SQLInstallTranslator 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 92ae84714ad78e6dca3a653b85b7815188c56756
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916793"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函式
**一致性**  
 版本引進了： ODBC 2.5，已被取代  
  
 **摘要**  
 在 ODBC 3.0 **SQLInstallTranslator**已被取代[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。 呼叫**SQLInstallTranslator**將會對應至**SQLInstallTranslatorEx**。 如需詳細資訊，請參閱**SQLInstallTranslatorEx**。  
  
 **SQLInstallTranslator**將傳回 FALSE，如果應用程式會呼叫它在 ODBC 3 *.x*驅動程式管理員與*lpszInfFile*引數設定為 NULL 以外的值。 使用 ODBC 2 Odbc.inf 檔案。*x*已不再支援在 ODBC 3 *.x*即使回溯相容性。
