---
title: 繫結資料行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88e3593276851b6ab38fde0472a70be31b7cbf34
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199458"
---
# <a name="binding-columns"></a>繫結資料行
從資料來源提取的資料會傳回在變數中，針對此目的已配置的應用程式的應用程式。 這可以完成之前，必須建立應用程式的關聯，或*繫結*，設定這些變數的結果資料行; 就概念而言，此程序等同於應用程式變數繫結至陳述式參數。 當應用程式會將變數繫結至結果集資料行時，它會描述該變數-地址、 資料型別，等位，驅動程式。 驅動程式會將此資訊儲存在結構中，它會維護該陳述式，並在擷取資料列，從資料行傳回值使用的資訊。  
  
 此章節包含下列主題。  
  
-   [繫結結果集資料行](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
