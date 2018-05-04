---
title: 轉譯程式安裝 Dll |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2aabec831ba9b623a24f261551684e9bb259e24
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="translator-setup-dlls"></a>轉譯程式安裝 Dll
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003，ODBC 隨附於 Windows 作業系統。 您只明確應該在舊版 Windows 上安裝 ODBC。  
  
 轉譯程式安裝程式 DLL 包含**ConfigTranslator**函式，以傳回轉譯器的預設選項。 必要時，它會提示使用者提供這項資訊。 如需此函式的完整說明，請參閱[安裝 DLL 應用程式開發介面參考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 轉譯程式安裝程式的 DLL 是轉譯程式開發人員所撰寫。 它可以轉譯程式的 DLL 或個別的 DLL。
