---
title: 桌面資料庫驅動程式相容性 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d081d53458ec59eb2ac9f05c5c1d47d6991b5010
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240354"
---
# <a name="desktop-database-driver-compatibility"></a>桌面資料庫驅動程式相容性
Unicode 是軟體的字元編碼的方法將所有字元視為擁有兩個位元組的固定的寬度。 這個方法用來替代 Windows ANSI 字元編碼方式，因為它代表一個位元組中的字元是限制為 256 個字元。 Unicode 可以代表 65,000 個字元，因為它所能容納的字元都不會出現的許多語言以 ANSI 編碼方式。  
  
 ODBC 3.5 （含） 以後的驅動程式管理員已啟用 Unicode。 這會影響兩個主要區域： 函式呼叫和字串資料類型。 驅動程式管理員對應函式的字串引數和所需的應用程式和驅動程式的字串資料，這兩者都可以啟用 Unicode 或 ANSI 啟用。  
  
 ODBC 3.5 （含） 以後的驅動程式管理員支援 Unicode 驅動程式與 Unicode 應用程式和 ANSI 應用程式的使用。 它也支援使用與 ANSI 應用程式的 ANSI 驅動程式。 驅動程式管理員提供有限的 Unicode-ANSI 對應 Unicode 應用程式使用的 ANSI 驅動程式。 這可讓 Jet 3.5 資料庫和所有現有的 ISAM 檔案類型的支援存取權。  
  
 當 ANSI 應用程式使用 ODBC 桌面資料庫驅動程式 4.0，並存取 Microsoft 存取 4.0 或更新版本中，驅動程式會將公開的資料類型為 SQL_CHAR、 SQL_VARCHAR 或 SQL_LONGVARCHAR 即使 Jet 4.0 支援的各種版本的功能。 SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR 不支援較舊版本的 Jet。 這項限制也適用於在其中會使用舊的格式與 Jet 4.0 資料庫引擎的情況下。  
  
 關於 ODBC Unicode 問題的詳細資訊，請參閱[Unicode](../../odbc/reference/develop-app/unicode.md)程式設計考量。
