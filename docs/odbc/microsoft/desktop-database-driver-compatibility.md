---
title: "桌面資料庫驅動程式相容性 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 34b9221b117819988e44196cee0f04578e85d436
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="desktop-database-driver-compatibility"></a>桌面資料庫驅動程式相容性
Unicode 是軟體的字元編碼的方法會將所有的字元視為具有兩個位元組的固定的寬度。 這個方法用做為 Windows ANSI 字元編碼、 替代其，因為它代表一個位元組中的字元限制為 256 個字元。 Unicode 可表示 65000 的字元，因為它可容納許多語言的字元都不會出現在 ANSI 編碼方式。  
  
 ODBC 3.5 （或更新版本） 驅動程式管理員與 Unicode 相容。 這會影響兩個主要區域： 函式呼叫和字串資料類型。 驅動程式管理員的對應函式的字串引數和字串資料所需的應用程式和驅動程式，這兩者都可以是 unicode 或 ANSI 啟用。  
  
 ODBC 3.5 （或更新版本） 驅動程式管理員支援 Unicode 驅動程式與在 Unicode 應用程式和 ANSI 應用程式的使用。 它也支援使用與 ANSI 應用程式的 ANSI 驅動程式。 驅動程式管理員會提供有限的 Unicode-ANSI 對應，以使用 ANSI 驅動程式在 Unicode 應用程式。 這可讓 Jet 3.5 資料庫和所有現有的 ISAM 檔案類型的支援人員的存取。  
  
 當 ANSI 應用程式使用 ODBC 桌面資料庫驅動程式 4.0，並存取 Microsoft 存取 4.0 或更新版本中，驅動程式公開的資料類型為 SQL_CHAR、 SQL_VARCHAR 或 SQL_LONGVARCHAR 即使 Jet 4.0 支援廣泛的版本。 SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR 不支援較舊的 Jet 版本。 這項限制也適用於舊的格式會使用與 Jet 4.0 資料庫引擎的情況下。  
  
 關於 ODBC Unicode 問題的詳細資訊，請參閱[Unicode](../../odbc/reference/develop-app/unicode.md)程式設計考量中。

