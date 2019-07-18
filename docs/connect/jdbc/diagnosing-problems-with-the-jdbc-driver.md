---
title: 診斷 JDBC driver 的問題 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 723e2680-a0c5-4a7d-a319-1e49e41078cf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b938a1e6e60307b991bf90d87673765f2efb01ef
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781973"
---
# <a name="diagnosing-problems-with-the-jdbc-driver"></a>診斷 JDBC Driver 的問題
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  不論應用程式的設計與開發有多好，都無法避免發生問題。 因此，發生問題時，具備診斷這些問題的一些技術十分重要。 使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 時，部分可能會發生的常見問題是因為沒有正確的驅動程式版本，或無法連線到資料庫。  
  
 本節中的主題討論診斷這些問題，以及包括錯誤處理、檢查驅動程式版本、追蹤和疑難排解連接問題之其他問題的多種技術。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[處理錯誤](../../connect/jdbc/handling-errors.md)|描述如何處理從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回的錯誤。|  
|[取得驅動程式版本](../../connect/jdbc/getting-the-driver-version.md)|描述如何判斷所安裝的 JDBC Driver 版本。|  
|[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)|描述如何在使用 JDBC 驅動程式時啟用追蹤功能。|  
|[針對連接性進行疑難排解](../../connect/jdbc/troubleshooting-connectivity.md)|描述如何疑難排解資料庫連接問題。|  
|[存取擴充事件記錄檔中的診斷資訊](../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md)|描述如何使用伺服器擴充事件記錄檔中的資訊，以了解連接失敗。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
