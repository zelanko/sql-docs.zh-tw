---
title: 剖析資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parsing [Integration Services]
- data parsing [Integration Services]
ms.assetid: 8893ea9d-634c-4309-b52c-6337222dcb39
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7517819f2cf6909cd95d76043519f78b06699b6c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136668"
---
# <a name="parsing-data"></a>剖析資料
  封裝中的資料流程會在異質資料存放區之間擷取和載入資料，這樣可以使用各種不同的標準和自訂資料類型。 在一個資料流程中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來源執行擷取資料、剖析字串資料並將資料轉換為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型的工作。 後續轉換可以剖析資料以便將其轉換成不同的資料類型，或者建立資料類型不同的資料行副本。 元件中使用的運算式同樣可以將引數和運算元轉換成不同的資料類型。 最後，當資料載入資料存放區時，目的地則可以剖析資料以便將其轉換成目的地使用的資料類型。 如需相關資訊，請參閱 [Integration Services Data Types](integration-services-data-types.md)。  
  
## <a name="types-of-parsing"></a>剖析的類型  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供兩種用於轉換資料的剖析類型：快速剖析和標準剖析。  
  
-   快速剖析是一組快速而簡單的剖析常式，它不支援地區設定特定的資料類型轉換，僅支援最常用的日期和時間格式。 如需相關資訊，請參閱 [Fast Parse](../fast-parse.md)。  
  
-   標準剖析是一組相當豐富的剖析常式，它支援由 Oleaut32.dll 和 Ole2dsip.dll 中可用的「自動」資料類型轉換 API 所提供的所有資料類型轉換。 如需相關資訊，請參閱 [Standard Parse](../standard-parse.md)。  
  
  