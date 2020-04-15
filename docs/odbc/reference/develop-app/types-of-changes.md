---
title: 變更類型 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f44adb59aa9b0f25475a76a97fe3670de0228c08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301603"
---
# <a name="types-of-changes"></a>變更的類型
在 ODBC *3.x(* 以及任何版本的 ODBC)中進行了三種類型的更改。 其中每種方法對向后相容性的影響都不同,並且以不同的方式處理。 下表描述了這些更改。  
  
|變更類型|描述|  
|--------------------|-----------------|  
|新功能|這些是 ODBC *3.x*的新功能,例如行外綁定或描述符。 僅當應用程式和驅動程式以及驅動程式管理器版本*3.x*時,才會實現這些版本,因此不會嘗試使這些向後相容。|  
|重複的功能|這些功能存在於 ODBC *2.x*和 ODBC *3.x*中,但在每個功能中以不同的方式實現。 **SQLAllocHandle**和**SQLAllocStmt**的函數就是一個例子。 這些和其他重複功能的向後相容性問題主要由驅動程式管理器中的映射處理。|  
|行為變更|這些功能在 ODBC *2.x*和 ODBC *3.x*中處理方式不同。 日期時間 **#define**就是一個例子。 這些功能由 ODBC *3.x*驅動程式根據環境屬性設置處理。 (有關詳細資訊,請參閱[行為更改](../../../odbc/reference/develop-app/behavioral-changes.md)。|
