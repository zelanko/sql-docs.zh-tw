---
description: 安裝程式 DLL API 參考
title: 設定 DLL API 參考 |Microsoft Docs
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
ms.openlocfilehash: 5cb3e20a1c25d206a1dd27367bbe4a128af0818f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487331"
---
# <a name="setup-dll-api-reference"></a>安裝程式 DLL API 參考
本節說明驅動程式安裝程式 DLL API 的語法，其中包含兩個函數 (**ConfigDriver** 和 **ConfigDSN**) 。 **ConfigDriver** 和 **ConfigDSN** 可以是在驅動程式 dll 或個別的安裝程式 dll 中。  
  
 此外，本節說明轉譯程式安裝程式 DLL API 的語法，其中包含單一函式 (**ConfigTranslator**) 。 **ConfigTranslator** 可以位於 translator dll 或個別的安裝程式 dll 中。  
  
 每個函式都會以它所引進之 ODBC 的版本戳記。  
  
 此章節包含下列主題。  
  
-   [ConfigDriver 函式](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [ConfigDSN 函式](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [ConfigTranslator 函式](../../../odbc/reference/syntax/configtranslator-function.md)
