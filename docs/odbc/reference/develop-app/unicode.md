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
ms.openlocfilehash: 7e0044a2e2efbf0d8921a07ed4679806ba50bcd1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087557"
---
# <a name="unicode"></a>Unicode
Unicode 會定義許多語言的字元編碼。  
  
 如需 Unicode 標準的詳細資訊，請參閱[Unicode 聯盟](https://www.unicode.org)。  
  
 Unicode 定義通用字元集。 Windows ANSI 字碼頁會定義一個字元集，其中通常包含一種語言的字元。 撰寫使用不同字碼頁所需的應用程式可能會比較棘手。  
  
 Unicode 不需要字碼頁。 每個程式碼點都會以某種語言對應至單一字元。  
  
 目前，ODBC 支援的唯一 Unicode 編碼是 UCS-2，它使用16位整數（固定長度）來代表字元。 Unicode 可讓應用程式使用不同的語言。  
  
 ODBC 3.5 （或更新版本）驅動程式管理員具有 Unicode 功能。 這會影響兩個主要區域：函式呼叫和字串資料類型。 驅動程式管理員會依照應用程式和驅動程式的需求來對應函式字串引數和字串資料，這兩者都可以是啟用 Unicode 或啟用 ANSI 功能。 這兩個區域會在「Unicode 函式[引數](../../../odbc/reference/develop-app/unicode-function-arguments.md)」和「 [unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)」小節中詳細討論。  
  
 ODBC 3.5 （或更新版本）驅動程式管理員支援使用 Unicode 驅動程式搭配 Unicode 應用程式和 ANSI 應用程式。 它也支援搭配 ANSI 應用程式使用 ANSI 驅動程式。 驅動程式管理員針對與 ANSI 驅動程式搭配使用的 Unicode 應用程式，提供有限的 Unicode 對 ANSI 對應。  
  
 此章節包含下列主題。  
  
-   [Unicode 函式引數](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)
