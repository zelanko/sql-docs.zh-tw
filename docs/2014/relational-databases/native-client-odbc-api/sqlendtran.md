---
title: SQLEndTran |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ec3c40d7821c86f3f5c5a7eb0d63ab48904513e2
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706269"
---
# <a name="sqlendtran"></a>SQLEndTran
  根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當**SQLEndTran**認可或回復作業時，Native Client ODBC 驅動程式會關閉語句的相關資料指標。 除非伺服器資料指標是靜態的，否則會關閉它們。 當**SQLEndTran**認可或回復作業時，語句相關資料指標的行為是由驅動程式特定的 ODBC 連接屬性值所決定，SQL_COPT_SS_PRESERVE_CURSORS，由[SQLSetConnectAttr](sqlsetconnectattr.md)設定。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 的執行詳細資料](odbc-api-implementation-details.md)   
 [SQLEndTran 函數](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
