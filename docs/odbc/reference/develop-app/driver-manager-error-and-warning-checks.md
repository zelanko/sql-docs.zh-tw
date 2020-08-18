---
description: 驅動程式管理員錯誤和警告檢查
title: 驅動程式管理員錯誤和警告檢查 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99a99e1dfeb6cb6993a6967d5d93748afbd44b83
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483051"
---
# <a name="driver-manager-error-and-warning-checks"></a>驅動程式管理員錯誤和警告檢查
驅動程式管理員完全或部分實行一些函數，因此會檢查這些函式中的所有或部分錯誤和警告。  
  
-   驅動程式管理員會執行 **SQLDataSources** 和 **SQLDrivers** ，並檢查這些函數中的所有錯誤和警告。  
  
-   驅動程式管理員會檢查驅動程式是否會執行 **SQLGetFunctions**。 如果驅動程式未執行 **SQLGetFunctions**，驅動程式管理員會執行並檢查其中的所有錯誤和警告。  
  
-   驅動程式管理員部分會執行 **SQLAllocHandle**、 **SQLConnect**、 **SQLDriverConnect**、 **SQLBrowseConnect**、 **SQLFreeHandle**、 **SQLGetDiagRec**和 **SQLGetDiagField** ，並檢查這些函式中是否有一些錯誤。 它可能會傳回與這些函式的驅動程式相同的錯誤，因為兩者都執行類似的作業。 例如，如果其中一項無法顯示 **SQLDriverConnect**的登入對話方塊，驅動程式管理員或驅動程式可能會傳回 SQLSTATE IM008 (對話失敗) 。
