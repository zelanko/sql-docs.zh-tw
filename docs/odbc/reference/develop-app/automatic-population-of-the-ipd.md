---
title: IPD 的自動填充 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1998ea1992ee7f14d87d01e348d955b017166088
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285068"
---
# <a name="automatic-population-of-the-ipd"></a>自動 IPD 擴展
在準備好參數化查詢後,某些驅動程式能夠設置 IPD 的欄位。 描述符欄位會自動填充有關參數的資訊,包括資料類型、精度、比例和其他特徵。 這相當於支援**SQLDescribeParam。** 當應用程式沒有其他方法發現此資訊時,例如使用應用程式不知道的參數執行臨時查詢時,此資訊對於應用程式來說可能特別有價值。  
  
 應用程式通過調用具有SQL_ATTR_AUTO_IPD*屬性*的**SQLGetConnectAttr**來確定驅動程式是否支援自動填充。 如果返回SQL_TRUE,驅動程式將支援它,應用程式可以通過將SQL_ATTR_ENABLE_AUTO_IPD語句屬性設置為SQL_TRUE來啟用它。  
  
 支援並啟用自動填充後,驅動程式在 SQL 語句透過調用**SQLPrepare**編寫後填充 IPD 的欄位。 應用程式可以通過調用**SQLGetDescField**或**SQLGetDescRec**或**SQLDescribeParam**來檢索此資訊。 應用程式可以使用資訊綁定參數最適當的應用程式緩衝區,或為其指定數據轉換。  
  
 IPD 的自動填充可能會產生性能損失。 應用程式可以通過將SQL_ATTR_ENABLE_AUTO_IPD語句屬性重置為SQL_FALSE(預設值)來將其關閉。
