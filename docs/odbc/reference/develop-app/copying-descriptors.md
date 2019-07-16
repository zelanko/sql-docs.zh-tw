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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002146"
---
# <a name="copying-descriptors"></a>複製描述項
**SQLCopyDesc**呼叫函式可將有一個描述項欄位複製到另一個描述元。 只有應用程式描述項或 IPD，但不是屬於 IRD，可以複製欄位。 欄位可以從任何類型的描述元複製。 只有在來源和目標的描述項所定義的欄位都會複製。 **SQLCopyDesc**不會複製 SQL_DESC_ALLOC_TYPE 欄位中，因為無法變更的描述元的配置類型。 複製的欄位覆寫現有的欄位。  
  
 上一個陳述式控制代碼 ARD 可做為另一個陳述式控制代碼上 APD。 這可讓應用程式複製資料表，而不複製應用程式層級的資料之間的資料列。 若要這樣做，資料列描述項所描述的資料表擷取的資料列會重複使用為 INSERT 陳述式中的參數的參數描述元。 SQL_MAX_CONCURRENT_ACTIVITIES 資訊型別必須是大於 1，這項作業才會成功。
