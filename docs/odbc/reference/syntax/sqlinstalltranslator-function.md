---
title: SQLInstallTranslator 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5b973332c2fe0fa541635d326a3a5adecf6ae91
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076108"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函式
**標準**  
 引進的版本： ODBC 2.5，已被取代  
  
 **摘要**  
 在 ODBC 3.0 中， **SQLInstallTranslator**已由[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)取代。 對**SQLInstallTranslator**的呼叫將會對應至**SQLInstallTranslatorEx**。 如需詳細資訊，請參閱**SQLInstallTranslatorEx**。  
  
 如果應用程式*在 ODBC 3.X*驅動程式管理員中呼叫它，並將*lpszInfFile*引數設為 Null 以外的值，則**SQLInstallTranslator**會傳回 FALSE。 Odbc 3.x*中已不再支援 odbc 2.x*中使用的 odbc .inf*檔案，即使*是回溯相容性也一樣。
