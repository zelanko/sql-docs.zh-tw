---
title: Unicode |微軟文件
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
ms.openlocfilehash: 9824e76cebabb6f5f84505292801a0094e359f0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302442"
---
# <a name="unicode"></a>Unicode
Unicode 定義多種語言中的字元的編碼。  
  
 有關 Unicode 標準的詳細資訊,請參閱[Unicode 聯盟](https://www.unicode.org)。  
  
 Unicode 定義通用字元集。 Windows ANSI 代碼頁定義一個字元集,通常包含一種語言的字元。 編寫需要使用不同的代碼頁的應用程式可能更加困難。  
  
 Unicode 不需要代碼頁。 每個代碼點都映射到一種語言的單個字元。  
  
 目前,ODBC 支援的唯一 Unicode 編碼是 UCS-2,它使用 16 位整數(固定長度)來表示字元。 Unicode 允許應用程式以不同的語言工作。  
  
 ODBC 3.5(或更高版本)驅動程式管理器啟用了 Unicode。 這會影響兩個主要區域:函數調用和字串數據類型。 驅動程式管理員根據應用程式和驅動程式的要求映射函數位串參數和字串資料,這兩個參數都可以啟用 Unicode 或啟用 ANSI。 這兩個區域將在[「Unicode 函數參數](../../../odbc/reference/develop-app/unicode-function-arguments.md)」和[「Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)」部分中詳細討論。  
  
 ODBC 3.5(或更高版本)驅動程式管理員支援將 Unicode 驅動程式與 Unicode 應用程式和 ANSI 應用程式一起使用。 它還支援將 ANSI 驅動程式與 ANSI 應用程式一起使用。 驅動程式管理員為使用 ANSI 驅動程式的 Unicode 應用程式提供有限的 Unicode 到 ANSI 映射。  
  
 此章節包含下列主題。  
  
-   [Unicode 函式引數](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)
