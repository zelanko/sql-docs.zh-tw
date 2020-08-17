---
description: 桌面資料庫驅動程式相容性
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b15ec35a01b61eef401f217733917a80bbe32b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340774"
---
# <a name="desktop-database-driver-compatibility"></a>桌面資料庫驅動程式相容性
Unicode 是一種軟體字元編碼方法，會將所有字元視為具有兩個位元組的固定寬度。 此方法是做為 Windows ANSI 字元編碼的替代方案，因為它代表一個位元組中的字元，限制為256個字元。 因為 Unicode 可代表超過65000個字元，所以它會容納許多語言，而這些語言的字元不會以 ANSI 編碼表示。  
  
 ODBC 3.5 (或更新版本) 驅動程式管理員已啟用 Unicode。 這會影響兩個主要區域：函式呼叫和字串資料類型。 驅動程式管理員會依應用程式和驅動程式的要求來對應函式字串引數和字串資料，兩者都可以是啟用 Unicode 或啟用 ANSI 功能。  
  
 ODBC 3.5 (或更新版本的) 驅動程式管理員支援使用 unicode 驅動程式搭配 Unicode 應用程式和 ANSI 應用程式。 它也支援使用 ANSI 驅動程式搭配 ANSI 應用程式。 驅動程式管理員可針對使用 ANSI 驅動程式的 Unicode 應用程式，提供有限的 Unicode 對 ANSI 對應。 這可讓您存取 Jet 3.5 資料庫，並支援所有現有的 ISAM 檔案類型。  
  
 當 ANSI 應用程式使用 ODBC Desktop 資料庫驅動程式4.0 並存取 Microsoft Access 4.0 或更新版本時，驅動程式會將資料類型公開為 SQL_CHAR、SQL_VARCHAR 或 SQL_LONGVARCHAR，即使 Jet 4.0 支援廣泛版本也是一樣。 舊版的 Jet 不支援 SQL_WCHAR、SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 這項限制也適用于舊版格式與 Jet 4.0 資料庫引擎搭配使用的情況。  
  
 如需 ODBC 的 Unicode 問題的詳細資訊，請參閱程式設計考慮中的 [unicode](../../odbc/reference/develop-app/unicode.md) 。
