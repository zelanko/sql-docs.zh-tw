---
title: 使用大型資料 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 126775f2b56bdf2cf1847334b0c8faad7cfcfafb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-large-data"></a>使用大型資料
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 驅動程式提供適應性緩衝的支援，可讓您擷取任何種類的大數值資料，而不會造成伺服器資料指標的負擔。 利用適應性緩衝，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]擷取陳述式執行結果從[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]應用程式需要時，而非一次。 只要應用程式不再存取這些結果，驅動程式也可以捨棄它們。  
  
 在[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)] JDBC Driver 1.2 版的緩衝模式為"**完整**」 預設。 如果您的應用程式未設定"responseBuffering"連接屬性"**適應性**"連接屬性中或使用[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件、 驅動程式支援一次從伺服器讀取整個結果。 為了取得適應性緩衝行為，您的應用程式必須將"responseBuffering"連接屬性設定為"**適應性**"明確。  
  
 **適應性**值為預設的緩衝模式，而且 JDBC 驅動程式的可能資料下限必要時緩衝處理。 如需有關使用適應性緩衝的詳細資訊，請參閱[使用適應性緩衝](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
 此章節的主題描述可用來擷取大數值資料的不同方式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[讀取大型資料範例](../../../connect/jdbc/reading-large-data-sample.md)|描述如何使用 SQL 陳述式來擷取大數值資料。|  
|[使用預存程序讀取大型資料範例](../../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)|描述如何擷取大型 CallableStatement OUT 參數值。|  
|[更新大型資料範例](../../../connect/jdbc/updating-large-data-sample.md)|描述如何更新資料庫中的大數值資料。|  
  
## <a name="see-also"></a>另請參閱  
 [範例 JDBC 驅動程式應用程式](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
