---
title: SQLFreeConnect 映射 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20da205d53acbebca1fee12134c04f17fb8b2db3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302039"
---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect 對應
當應用程式透過 ODBC *3.x*驅動程式呼叫**SQLFreeConnect**時,呼叫  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 對應  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 將*Handle*參數設定為*hdbc*中的值。
