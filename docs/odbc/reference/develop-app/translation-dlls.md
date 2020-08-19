---
description: 轉譯 DLL
title: 轉譯 Dll |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88e0fc6879db7e4b370acc62b2d0102b3ef0a375
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421452"
---
# <a name="translation-dlls"></a>轉譯 DLL
應用程式和資料來源通常會將資料儲存在不同的字元集。 ODBC 提供一般機制，可讓驅動程式將資料從一個字元集轉譯成另一個字元集。 它是由一個 DLL 所組成，此 DLL 會執行轉譯函式 **SQLDriverToDataSource** 和 **SQLDataSourceToDriver**，由驅動程式呼叫，以轉譯資料來源和驅動程式之間的所有資料流程動。 應用程式開發人員、驅動程式開發人員或協力廠商可以撰寫這個 DLL。  
  
 您可以在該資料來源的系統資訊中指定特定資料來源的轉譯 DLL;如需詳細資訊，請參閱 [資料來源規格](../../../odbc/reference/install/data-source-specification-subkeys.md)子機碼。 您也可以在執行時間使用 SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION 連接屬性來設定它。  
  
 轉譯選項是只能由特定轉譯 DLL 來解讀的值。 例如，如果翻譯 DLL 在不同的字碼頁之間轉譯，則選項可能會提供應用程式和資料來源所使用的字碼頁編號。 轉譯 DLL 不需要使用轉譯選項。  
  
 指定轉譯 DLL 之後，驅動程式會將它載入，並呼叫它來轉譯應用程式與資料來源之間的所有資料。 這包括要傳送到資料來源的所有 SQL 語句和字元參數，以及所有字元結果、字元中繼資料（例如資料行名稱），以及從資料來源取出的錯誤訊息。 連接資料不會轉譯，因為在應用程式連接到資料來源之前，不會載入轉譯 DLL。
