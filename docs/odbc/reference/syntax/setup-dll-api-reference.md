---
title: 設定 DLL API 參考 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25cff50b73868b5b3015dfc1a00c560c344a6d36
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298883"
---
# <a name="setup-dll-api-reference"></a>安裝程式 DLL API 參考
本節介紹驅動程式設置 DLL API 的語法,它由兩個函數(**配置驅動程式**和**配置DSN)** 組成。 **配置驅動程式**和**配置DSN**可以位於驅動程式 DLL 中,也可以位於單獨的設置 DLL 中。  
  
 此外,本節還介紹譯者設置 DLL API 的語法,該 API 由單個函數(**配置轉換器**)組成。 **配置轉換器**可以位於轉換器 DLL 中,也可以位於單獨的設置 DLL 中。  
  
 每個函數都標有引入該函數的 ODBC 版本。  
  
 此章節包含下列主題。  
  
-   [ConfigDriver 函式](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [ConfigDSN 函式](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [ConfigTranslator 函式](../../../odbc/reference/syntax/configtranslator-function.md)
