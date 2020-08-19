---
description: SQLInstallTranslator 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0be53f18682290c976af73c214d9f87b01b84704
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421152"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函式
**一致性**  
 引進的版本： ODBC 2.5，已淘汰  
  
 **總結**  
 在 ODBC 3.0 中， **SQLInstallTranslator** 已由 [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)取代。 對 **SQLInstallTranslator** 的呼叫會對應至 **SQLInstallTranslatorEx**。 如需詳細資訊，請參閱 **SQLInstallTranslatorEx**。  
  
 如果應用程式*在 ODBC 3.X*驅動程式管理員中呼叫它，並將*lpszInfFile*引數設定為 Null 以外的值，則**SQLInstallTranslator**會傳回 FALSE。 Odbc 2.x 不再支援 odbc 2.x 中使用的 Odbc .inf*檔案，即使*是回溯相容性*也是如此*。
