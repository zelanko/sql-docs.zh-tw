---
title: 複製描述項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d41cd744d39113c556c4ee8bc17411b7992e596
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002146"
---
# <a name="copying-descriptors"></a>複製描述項
呼叫**SQLCopyDesc**函數，將一個描述元的欄位複製到另一個描述項。 欄位只能複製到應用程式描述元或 IPD，但不能複製到 IRD。 可以從任何類型的描述項複製欄位。 只會複製為來源和目標描述元定義的欄位。 **SQLCopyDesc**不會複製 SQL_DESC_ALLOC_TYPE 欄位，因為無法變更描述項的配置類型。 複製的欄位會覆寫現有的欄位。  
  
 一個語句控制碼上的 ARD 可作為另一個語句控制碼上的 APD。 這可讓應用程式在資料表之間複製資料列，而不需要在應用層級複製資料。 若要這樣做，描述資料表之提取資料列的資料列描述元會重複使用，做為 INSERT 語句中參數的參數描述元。 SQL_MAX_CONCURRENT_ACTIVITIES 資訊類型必須大於1，此作業才會成功。
