---
title: 驅動程式管理員錯誤和警告檢查 |微軟文件
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
ms.openlocfilehash: ee8a0f5ebfac8b6f87281806f07989f4980eb9b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305780"
---
# <a name="driver-manager-error-and-warning-checks"></a>驅動程式管理員錯誤和警告檢查
驅動程式管理員全部或部分實現許多功能,因此檢查這些函數中的所有或某些錯誤和警告。  
  
-   驅動程式管理員實現**SQLDataSources**和**SQLDriver,** 並檢查這些函數中的所有錯誤和警告。  
  
-   驅動程式管理員檢查驅動程式是否實現**SQLGet 函數**。 如果驅動程式未實現**SQLGet 功能**,驅動程式管理器將實現並檢查其中的所有錯誤和警告。  
  
-   驅動程式管理器部分實現**SQLAllocHandle、** **SQLConnect**, **SQLDriverConnect,** **SQLBrowseConnect、** **SQLFreeHandle、** **SQLGetDiagRec**和**SQLGetDiagField,** 並檢查這些函數中的一些錯誤。 對於其中一些函數,它可能會返回與驅動程式相同的錯誤,因為兩者都執行類似的操作。 例如,如果任一驅動程式無法顯示**SQLDriverConnect**的登入對話框,則驅動程式管理器或驅動程式可能會返回 SQLSTATE IM008(對話框失敗)。
