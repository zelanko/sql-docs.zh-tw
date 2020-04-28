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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89eea7ab112eaefdc73c7cbc72ee3555797c7efd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303519"
---
# <a name="desktop-database-driver-compatibility"></a>桌面資料庫驅動程式相容性
Unicode 是一種軟體字元編碼方法，會將所有字元視為具有兩個位元組的固定寬度。 這個方法是做為 Windows ANSI 字元編碼的替代方案，因為它代表一個位元組中的字元，所以只能使用256個字元。 因為 Unicode 可以代表超過65000個字元，所以它會容納許多字元不以 ANSI 編碼方式表示的語言。  
  
 ODBC 3.5 （或更新版本）驅動程式管理員具有 Unicode 功能。 這會影響兩個主要區域：函式呼叫和字串資料類型。 驅動程式管理員會依照應用程式和驅動程式的需求來對應函式字串引數和字串資料，這兩者都可以是啟用 Unicode 或啟用 ANSI 功能。  
  
 ODBC 3.5 （或更新版本）驅動程式管理員支援使用 Unicode 驅動程式搭配 Unicode 應用程式和 ANSI 應用程式。 它也支援搭配 ANSI 應用程式使用 ANSI 驅動程式。 驅動程式管理員針對與 ANSI 驅動程式搭配使用的 Unicode 應用程式，提供有限的 Unicode 對 ANSI 對應。 這可讓您存取 Jet 3.5 資料庫，並支援所有現有的 ISAM 檔案類型。  
  
 當 ANSI 應用程式使用 ODBC 桌面資料庫驅動程式4.0 並存取 Microsoft Access 4.0 或更新版本時，驅動程式會將資料類型公開為 SQL_CHAR、SQL_VARCHAR 或 SQL_LONGVARCHAR，即使 Jet 4.0 支援寬版本也一樣。 較舊版本的 Jet 不支援 SQL_WCHAR、SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 這項限制也適用于舊版格式與 Jet 4.0 資料庫引擎搭配使用的情況。  
  
 如需有關 ODBC Unicode 問題的詳細資訊，請參閱程式設計考慮中的[unicode](../../odbc/reference/develop-app/unicode.md) 。
