---
title: 固定長度書簽 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5877a6cb7a99803f854338321e333c87037c2e90
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67913578"
---
# <a name="fixed-length-bookmarks"></a>固定長度書籤
如果 ODBC 3.x*驅動程式*應該搭配使用固定長度書簽的 odbc 2.x*應用程式*使用，則驅動程式必須支援下列各項：  
  
-   SQL_UB_ON 做為 SQL_USE_BOOKMARKS 語句選項的值。 （SQL_UB_ON*在 ODBC 3.x*中被取代）。  
  
-   SQL_GET_BOOKMARK 語句選項。
