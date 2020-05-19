---
title: 資料指標並行（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7139ace2498ef2eeddb173950281ac4cf493efad
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705588"
---
# <a name="cursor-concurrency-odbc"></a>資料指標並行 (ODBC)
  資料指標作業跟資料指標類型一樣，會受到應用程式設定之並行選項的影響。 並行選項是使用[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)的 SQL_ATTR_CONCURRENCY 選項來設定。 並行類型為：  
  
-   唯讀 (SQL_CONCUR_READONLY)  
  
-   值 (SQL_CONCUR_VALUES)  
  
-   資料列版本 (SQL_CONCUR_ROWVER)  
  
-   鎖定 (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>另請參閱  
 [資料指標屬性](cursor-properties.md)  
  
  
