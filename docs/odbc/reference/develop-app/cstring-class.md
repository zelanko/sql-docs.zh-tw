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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0f941061bf1bc7671d4744d309770fc92c95dd6e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301647"
---
# <a name="cstring-class"></a>CString 類別
由於 Microsoft® Visual C++®中**CString**類別的物件是已簽署的，而且 ODBC 函式中的字串引數不帶正負號，將**CString**物件傳遞至 odbc 函式而不進行轉換的應用程式將會收到編譯器警告。
