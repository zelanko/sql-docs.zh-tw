---
title: Unicode |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e6201b83b909573476b043cdb1a10543f894def
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661807"
---
# <a name="unicode"></a>Unicode
Unicode 定義許多語言的字元編碼方式。  
  
 如需 Unicode 標準的詳細資訊，請參閱[Unicode 協會](https://www.unicode.org)。  
  
 Unicode 定義通用的字元集。 Windows ANSI 字碼頁定義的字元集，通常包含一種語言的字元。 它可能是更難撰寫的應用程式，才可使用不同的字碼頁。  
  
 Unicode 不需要的字碼頁。 每個字碼指標對應到某些語言中的單一字元。  
  
 目前，唯一的 Unicode 編碼 ODBC 支援是 UCS-2，這會使用 16 位元整數 （固定長度） 來表示字元。 Unicode 允許以不同語言工作的應用程式。  
  
 ODBC 3.5 （或更新版本） 驅動程式管理員已啟用 Unicode。 這會影響兩個主要區域： 函式呼叫和字串資料類型。 驅動程式管理員對應函式的字串引數和所需的應用程式和驅動程式的字串資料，這兩者都可以啟用 Unicode 或 ANSI 啟用。 這兩個區域中的各節將詳細討論[Unicode 函式引數](../../../odbc/reference/develop-app/unicode-function-arguments.md)並[Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 ODBC 3.5 （或更新版本） 驅動程式管理員支援 Unicode 驅動程式與 Unicode 應用程式和 ANSI 應用程式的使用。 它也支援使用與 ANSI 應用程式的 ANSI 驅動程式。 驅動程式管理員提供有限的 Unicode-ANSI 對應 Unicode 應用程式使用的 ANSI 驅動程式。  
  
 此章節包含下列主題。  
  
-   [Unicode 函式引數](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)
