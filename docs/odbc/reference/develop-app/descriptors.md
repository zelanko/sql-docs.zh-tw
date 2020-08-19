---
description: 描述項
title: 描述項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae01f093ef1b67f1326f8aa7719b74100fcba462
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429330"
---
# <a name="descriptors"></a>描述項
描述項控制碼指的是保存資料行或動態參數相關資訊的資料結構。  
  
 在資料行和參數資料上操作的 ODBC 函數會隱含地設定和取出描述項欄位。 比方說，當呼叫 **SQLBindCol** 來系結資料行資料時，它會設定完全描述系結的描述項欄位。 當呼叫 **SQLColAttribute** 來描述資料行資料時，它會傳回儲存在描述項欄位中的資料。  
  
 呼叫 ODBC 函數的應用程式不需要與描述項一起關注。 沒有任何資料庫作業需要應用程式直接存取描述項。 不過，針對某些應用程式，取得可直接存取描述項可簡化許多作業。 例如，直接存取描述項可提供重新系結資料行資料的方式，這比再次呼叫 **SQLBindCol** 更有效率。  
  
> [!NOTE]  
>  未定義描述項的實體標記法。 應用程式只能藉由使用描述項控制碼來呼叫 ODBC 函數，藉以直接存取描述項。  
  
 此章節包含下列主題。  
  
-   [描述項的類型](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [描述項欄位](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [配置及釋放描述項](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [取得並設定描述項欄位](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
