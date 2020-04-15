---
title: 桌面資料庫驅動程式相容性 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89eea7ab112eaefdc73c7cbc72ee3555797c7efd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303519"
---
# <a name="desktop-database-driver-compatibility"></a>桌面資料庫驅動程式相容性
Unicode 是一種軟體字元編碼方法,它將所有字元視為具有兩個字節的固定寬度。 此方法用作 Windows ANSI 字元編碼的替代方法,由於它表示一個字節中的字元,因此限制為 256 個字元。 由於 Unicode 可以表示超過 65,000 個字元,因此它適合許多字元在 ANSI 編碼中未表示的語言。  
  
 ODBC 3.5(或更高版本)驅動程式管理員已啟用 Unicode。 這會影響兩個主要區域:函數調用和字串數據類型。 驅動程式管理員根據應用程式和驅動程式的要求映射函數位串參數和字串資料,這兩個參數都可以啟用 Unicode 或啟用 ANSI。  
  
 ODBC 3.5(或更高版本)驅動程式管理員支援將 Unicode 驅動程式與 Unicode 應用程式和 ANSI 應用程式一起使用。 它還支援將 ANSI 驅動程式與 ANSI 應用程式一起使用。 驅動程式管理員為使用 ANSI 驅動程式的 Unicode 應用程式提供有限的 Unicode 到 ANSI 映射。 這允許存取 Jet 3.5 資料庫並支援所有現有的 ISAM 檔案類型。  
  
 當 ANSI 應用程式使用 ODBC 桌面資料庫驅動程式 4.0 並訪問 Microsoft Access 4.0 或更高版本時,驅動程式將數據類型公開為SQL_CHAR、SQL_VARCHAR或SQL_LONGVARCHAR,即使 Jet 4.0 支援寬版本。 舊版本的 Jet 不支援SQL_WCHAR、SQL_WVARCHAR和SQL_WLONGVARCHAR。 此限制也適用於舊格式與 Jet 4.0 資料庫引擎一起使用的情況。  
  
 有關 ODBC 的 Unicode 問題的詳細資訊,請參閱程式設計注意事項中的[Unicode。](../../odbc/reference/develop-app/unicode.md)
