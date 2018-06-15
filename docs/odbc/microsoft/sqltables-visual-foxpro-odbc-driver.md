---
title: SQLTables （Visual FoxPro ODBC 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8eccd686c1c4e3226a929cb39ee16e1921435ca
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32903443"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 完整  
  
 ODBC 應用程式開發介面相容性： 層級 1  
  
 傳回清單中的參數所指定的資料表名稱**SQLTables**陳述式。 如果未不指定任何參數，會傳回儲存在目前的資料來源中的資料表名稱。 驅動程式會傳回結果集的資訊。  
  
 列舉型別呼叫不會接收結果集項目，檢視遠端或本機參數化的檢視。 不過，呼叫**SQLTables**與唯一資料表名稱規範會發現這種檢視的相符項目如果存在具有該名稱，這可讓用來檢查是否有名稱衝突之前建立之新資料表的, API。  
  
> [!NOTE]  
>  Visual FoxPro ODBC 驅動程式區別[資料庫資料表](../../odbc/microsoft/visual-foxpro-terminology.md)和[釋放資料表](../../odbc/microsoft/visual-foxpro-terminology.md)，即使這兩類資料表會儲存在您的系統上相同的目錄。 如果您的資料來源是可用的資料表的目錄，Visual FoxPro ODBC 驅動程式不目錄或傳回與資料庫相關聯的任何資料表的名稱。  
  
 如需詳細資訊，請參閱[SQLTables](../../odbc/reference/syntax/sqltables-function.md)中*ODBC 程式設計人員參考*。
