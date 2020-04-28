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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f90c5888a68506c056b2a56fce516080148528e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306979"
---
# <a name="fixed-length-bookmarks"></a>固定長度書籤
如果 ODBC 3.x*驅動程式*應該搭配使用固定長度書簽的 odbc 2.x*應用程式*使用，則驅動程式必須支援下列各項：  
  
-   SQL_UB_ON 做為 SQL_USE_BOOKMARKS 語句選項的值。 （SQL_UB_ON*在 ODBC 3.x*中被取代）。  
  
-   SQL_GET_BOOKMARK 語句選項。
