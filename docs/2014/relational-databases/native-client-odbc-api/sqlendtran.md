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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5425fdc189febd23e9fc61765f4ad56fe484111
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067585"
---
# <a name="sqlendtran"></a>SQLEndTran
  根據預設，當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQLEndTran**認可或回復作業時，Native Client ODBC 驅動程式會關閉語句的相關資料指標。 除非伺服器資料指標是靜態的，否則會關閉它們。 當**SQLEndTran**認可或回復作業時，語句相關資料指標的行為是由驅動程式特定的 ODBC 連接屬性值所決定，SQL_COPT_SS_PRESERVE_CURSORS，由[SQLSetConnectAttr](sqlsetconnectattr.md)設定。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 的執行詳細資料](odbc-api-implementation-details.md)   
 [SQLEndTran 函數](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
