---
description: 參數標記
title: 參數標記 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: a585fb983a8f1662cdd42d361f106a76bfd47cb6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483231"
---
# <a name="parameter-markers"></a>參數標記
根據 SQL-92 規格，應用程式無法將參數標記放置於下列位置。 如需更完整的清單，請參閱 SQL-92 規格。  
  
-   在 **選取** 清單中  
  
-   做為*比較*述詞中的兩個*運算式*  
  
-   As 二元運算子的兩個運算元  
  
-   作為 **BETWEEN** 作業的第一個和第二個運算元  
  
-   作為 **BETWEEN** 作業的第一個和第三個運算元  
  
-   同時做為運算的運算式和**第一個值**  
  
-   作為一元 + 或-運算的運算元  
  
-   做為*集合函數-參考*的引數  
  
 如需參數標記的詳細資訊，請參閱 SQL-92 規格。 如需參數的詳細資訊，請參閱 [語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。
