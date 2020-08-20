---
description: 轉譯程式安裝程式 DLL
title: Translator 安裝程式 Dll |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fe4d514f098773024392666d8f528592d362da4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487391"
---
# <a name="translator-setup-dlls"></a>轉譯程式安裝程式 DLL
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統中。 您應該只在舊版的 Windows 上明確地安裝 ODBC。  
  
 轉譯程式安裝程式 DLL 包含 **ConfigTranslator** 函式，此函式會傳回翻譯工具的預設選項。 如有必要，它會提示使用者提供此資訊。 如需此功能的完整說明，請參閱 [安裝程式 DLL API 參考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 Translator 安裝程式 DLL 是由 translator developer 撰寫的。 它可以是翻譯工具 DLL 的一部分或個別的 DLL。
