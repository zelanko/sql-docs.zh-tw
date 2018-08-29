---
title: 使用大型資料 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
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
ms.openlocfilehash: 728e86f155a1bb61c7fe900f5e536eed991c206a
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784376"
---
# <a name="working-with-large-data"></a>使用大型資料

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

JDBC 驅動程式提供適應性緩衝的支援，可讓您擷取任何種類的大數值資料，而不會造成伺服器資料指標的負擔。 利用自適性緩衝，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 會在應用程式需要時，從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 擷取陳述式執行結果，而非一次擷取所有結果。 只要應用程式不再存取這些結果，驅動程式也可以捨棄它們。  
  
在 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] JDBC 驅動程式 1.2 版中，預設的緩衝模式為 "**full**"。 如果您的應用程式並未在連接屬性中或使用 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法，將 "responseBuffering" 連接屬性設定為 "**adaptive**"，此驅動程式就會支援一次從伺服器中讀取完整的結果。 為了取得適應性緩衝行為，您的應用程式必須明確將 "responseBuffering" 連接屬性設定為 "**adaptive**"。  
  
**adaptive** 值就是預設的緩衝模式，而且 JDBC 驅動程式會在必要時緩衝處理最少的可能資料。 如需有關使用適應性緩衝的詳細資訊，請參閱[使用適應性緩衝](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
本節中的主題將描述一些不同的方法，讓您可以用來從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中擷取大數值資料。  
  
## <a name="in-this-section"></a>本節內容  
  
| 主題                                                                                                                         | Description                                                              |
| ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [讀取大型資料範例](../../../connect/jdbc/code-samples/reading-large-data-sample.md)                                               | 描述如何使用 SQL 陳述式來擷取大數值資料。       |
| [使用預存程序讀取大型資料範例](../../../connect/jdbc/code-samples/reading-large-data-with-stored-procedures-sample.md) | 描述如何擷取大型 CallableStatement OUT 參數值。 |
| [更新大型資料範例](../../../connect/jdbc/code-samples/updating-large-data-sample.md)                                             | 描述如何更新資料庫中的大數值資料。                |
  
## <a name="see-also"></a>另請參閱

[範例 JDBC 驅動程式應用程式](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
  