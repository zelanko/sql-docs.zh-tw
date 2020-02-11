---
title: 安裝程式 DLL API 參考 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26e5c36b41f68627a634714cfa06525c99451450
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947059"
---
# <a name="setup-dll-api-reference"></a>安裝程式 DLL API 參考
本節說明驅動程式安裝程式 DLL API 的語法，其中包含兩個函式（**ConfigDriver**和**ConfigDSN**）。 **ConfigDriver**和**ConfigDSN**可以位於驅動程式 dll 或個別安裝程式 dll 中。  
  
 此外，本節也會說明 translator 安裝程式 DLL API 的語法，其中包含單一函式（**ConfigTranslator**）。 **ConfigTranslator**可以位於 translator dll 或個別安裝程式 dll 中。  
  
 每個函式都會標示其引進的 ODBC 版本。  
  
 此章節包含下列主題。  
  
-   [ConfigDriver 函式](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [ConfigDSN 函式](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [ConfigTranslator 函式](../../../odbc/reference/syntax/configtranslator-function.md)
