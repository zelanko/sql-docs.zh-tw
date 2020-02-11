---
title: ODBC 測試 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC test [ODBC]
- ODBC drivers [ODBC], testing
- gtrtst32.dll
- gtrts32w.dll [ODBC]
- odbct32w.exe [ODBC]
- odbcte32.exe [ODBC]
- testing ODBC drivers [ODBC]
ms.assetid: 7f13894c-5697-436c-be3d-fe16e1a02325
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a95e1798758aa044df5196f621c6afa14958c5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996284"
---
# <a name="odbc-test"></a>ODBC 測試
Microsoft® ODBC 測試是啟用 ODBC 的應用程式，可用來測試 ODBC 驅動程式和 ODBC 驅動程式管理員。 ODBC 3.51 包括 ANSI 和啟用 Unicode 的 ODBC 測試版本。 對應的檔案如下所示：  
  
-   Odbcte32 .exe 和 Gtrtst32，適用于 ANSI 版本。  
  
-   Odbct32w .exe 和 Gtrts32w，適用于 Unicode 版本。  
  
 若要使用 ODBC 測試，您必須瞭解 ODBC API、C 語言和 SQL。 如需 ODBC API 的詳細資訊，請參閱[odbc 程式設計人員參考](../odbc/reference/odbc-programmer-s-reference.md)。  
  
 先前包含在檔的這一節中的說明主題現在包含在 ODBC 測試程式中。 開啟 **[Odbcte32** ] 或 [Odbct32w]，開啟 [說明] 功能表，然後按一下 [**說明主題**]。  
  
 請注意，這些應用程式的64位版本（適用于64位 Microsoft Windows 作業系統）與32位版本具有相同的名稱，即使它們是不同的檔案。 亦即，Unicode 版本之64位版本的 ODBC 測試的名稱是 odbct32w。
