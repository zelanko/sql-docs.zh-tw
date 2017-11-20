---
title: "Unicode |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7ec40cc841c073fe66f9537687516f044048a0fc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="unicode"></a>Unicode
Unicode 定義許多語言的字元編碼方式。  
  
 如需 Unicode 標準的詳細資訊，請參閱[Unicode Consortium](http://www.unicode.org)。  
  
 Unicode 定義通用的字元集。 Windows ANSI 字碼頁定義字元集，通常包含一種語言的字元。 它可能會更難撰寫的應用程式，才能使用不同的字碼頁。  
  
 Unicode 不需要的字碼頁。 每個字碼指標對應到某些語言中的單一字元。  
  
 目前，唯一的 Unicode 編碼 ODBC 支援是 ucs-2、 其使用的 16 位元整數 （固定長度） 來表示字元。 Unicode 可讓應用程式在不同的語言運作。  
  
 ODBC 3.5 （或更新版本） 驅動程式管理員與 Unicode 相容。 這會影響兩個主要區域： 函式呼叫和字串資料類型。 驅動程式管理員的對應函式的字串引數和字串資料所需的應用程式和驅動程式，這兩者都可以是 unicode 或 ANSI 啟用。 在區段中，將詳細討論這兩個區域[Unicode 函式引數](../../../odbc/reference/develop-app/unicode-function-arguments.md)和[Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 ODBC 3.5 （或更新版本） 驅動程式管理員支援 Unicode 驅動程式與在 Unicode 應用程式和 ANSI 應用程式的使用。 它也支援使用與 ANSI 應用程式的 ANSI 驅動程式。 驅動程式管理員會提供有限的 Unicode-ANSI 對應，以使用 ANSI 驅動程式在 Unicode 應用程式。  
  
 此章節包含下列主題。  
  
-   [Unicode 函式引數](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)

