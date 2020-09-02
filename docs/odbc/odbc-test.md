---
description: ODBC 測試是具有 ODBC 功能的應用程式，可讓您用來測試 ODBC 驅動程式和 ODBC 驅動程式管理員。
title: ODBC 測試
ms.custom: ''
ms.date: 09/01/2020
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39869fe1230be75d9a76e13b8ba3938ec31ee5ee
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288243"
---
# <a name="odbc-test"></a>ODBC 測試

## <a name="about"></a>關於

Microsoft® ODBC 測試是啟用 ODBC 的應用程式，可讓您用來測試 ODBC 驅動程式和 ODBC 驅動程式管理員。 ODBC 測試隨附于 [Microsoft Data Access Components (MDAC) 2.8 軟體發展工具組](https://www.microsoft.com/download/details.aspx?id=21995)中。

ODBC 3.51 包含 ANSI 和啟用 Unicode 的 ODBC 測試版本。 對應的檔案如下所示：

- `Odbcte32.exe` 以及 `Gtrtst32.dll` ANSI 版本的。

- `Odbct32w.exe` 以及 `Gtrts32w.dll` Unicode 版本的。

若要使用 ODBC 測試，您必須瞭解 ODBC API、C 語言和 SQL。 如需 ODBC API 的詳細資訊，請參閱《 Odbc 程式設計 [人員參考](../odbc/reference/odbc-programmer-s-reference.md)》。

先前包含在此檔區段中的說明主題現在包含在 ODBC 測試程式中。 開啟 `Odbcte32.exe` 或開啟 [說明] `Odbct32w.exe` 功能表，然後按一下 [**說明主題**]。 **Help**

請注意，這些應用程式的64位版本（適用于64位 Microsoft Windows 作業系統）與32位版本具有相同的名稱，即使它們是不同的檔案。 亦即，ODBC 測試64位版本的 Unicode 版本名稱為 `odbct32w.exe` 。

## <a name="open-source"></a>開放原始碼

ODBC 測試是開放原始碼。 若要自行查看程式碼並建立最新版本的 ODBC 測試，請移至 [GitHub 儲存機制以進行 Odbc 測試](https://github.com/microsoft/ODBCTest)。
