---
description: Unicode
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a09a2647175d2b19aa44f1458d0ae8c4ef4565c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424430"
---
# <a name="unicode"></a>Unicode
Unicode 會定義許多語言字元的編碼方式。  
  
 如需 Unicode 標準的詳細資訊，請參閱 [Unicode 協會](https://www.unicode.org)。  
  
 Unicode 會定義通用字元集。 Windows ANSI 字碼頁會定義一組字元集，通常包含一種語言的字元。 撰寫使用不同字碼頁所需的應用程式可能會比較困難。  
  
 Unicode 不需要字碼頁。 每個程式碼點都會對應到某些語言的單一字元。  
  
 目前，ODBC 支援的 Unicode 編碼是 UCS-2，它使用16位整數 (固定長度) 來代表字元。 Unicode 可讓應用程式使用不同的語言。  
  
 ODBC 3.5 (或更新版本) 驅動程式管理員已啟用 Unicode。 這會影響兩個主要區域：函式呼叫和字串資料類型。 驅動程式管理員會依應用程式和驅動程式的要求來對應函式字串引數和字串資料，兩者都可以是啟用 Unicode 或啟用 ANSI 功能。 這兩個區域會在下列各節中詳細討論： [Unicode 函數引數](../../../odbc/reference/develop-app/unicode-function-arguments.md) 和 [unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 ODBC 3.5 (或更高版本的) 驅動程式管理員支援使用 unicode 驅動程式搭配 Unicode 應用程式和 ANSI 應用程式。 它也支援使用 ANSI 驅動程式搭配 ANSI 應用程式。 驅動程式管理員可針對使用 ANSI 驅動程式的 Unicode 應用程式，提供有限的 Unicode 對 ANSI 對應。  
  
 此章節包含下列主題。  
  
-   [Unicode 函式引數](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)
