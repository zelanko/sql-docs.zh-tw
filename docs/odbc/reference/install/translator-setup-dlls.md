---
title: 轉譯程式安裝程式 Dll |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20453b792ed00b388977fefe3064fd8dfca86147
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610126"
---
# <a name="translator-setup-dlls"></a>轉譯程式安裝程式 DLL
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統。 您只明確應該安裝在舊版 Windows 上的 ODBC。  
  
 轉譯程式安裝程式 DLL 包含**ConfigTranslator**函式，它會傳回轉換程式的預設選項。 如有必要，它會提示使用者提供這項資訊。 如需此函式的完整說明，請參閱[安裝程式 DLL API 參考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 轉譯程式安裝程式 DLL 是由轉譯程式開發人員撰寫。 它可以是轉譯程式組件 DLL 或不同的 DLL。
