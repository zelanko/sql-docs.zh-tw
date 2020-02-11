---
title: CString 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90c92476337bb1059b7272830e33094edc58dbd9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002076"
---
# <a name="cstring-class"></a>CString 類別
由於 Microsoft® Visual C++®中**CString**類別的物件是已簽署的，而且 ODBC 函式中的字串引數不帶正負號，將**CString**物件傳遞至 odbc 函式而不進行轉換的應用程式將會收到編譯器警告。
