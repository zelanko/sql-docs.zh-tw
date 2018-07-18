---
title: SQLEndTran |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99f4c5a37cc16cfce70545e6f74822da97ad0637
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408103"
---
# <a name="sqlendtran"></a>SQLEndTran
  根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會關閉的陳述式相關聯的資料指標時**SQLEndTran**認可或回復作業。 除非伺服器資料指標是靜態的，否則會關閉它們。 當**SQLEndTran**認可或回復作業，此陳述式相關聯的資料指標的行為取決於所設定的驅動程式專屬ODBC連接屬性SQL_COPT_SS_PRESERVE_CURSORS的值[SQLSetConnectAttr](sqlsetconnectattr.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)   
 [SQLEndTran 函式](http://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
