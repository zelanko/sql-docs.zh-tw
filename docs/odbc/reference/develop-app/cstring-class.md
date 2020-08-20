---
description: CString 類別
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
ms.openlocfilehash: cfe8809fed17e4e787c9965f175c4b97238868bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499931"
---
# <a name="cstring-class"></a>CString 類別
因為 Microsoft® Visual C++®中的 **CString** 類別的物件是未經簽署的，且 ODBC 函式中的字串引數未簽署，所以將 **CString** 物件傳遞給 odbc 函式而不加以轉換的應用程式將會收到編譯器警告。
