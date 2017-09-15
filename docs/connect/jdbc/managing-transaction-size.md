---
title: "管理交易大小 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 82900342-bc80-445f-98a4-468a303aae1e
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b333a2aa36c2dd7f2cd0e0065a955455549a813e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="managing-transaction-size"></a>管理交易大小
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當您使用交易時，盡可能讓交易越簡短越好相當重要。 自動認可，您可以啟用或停用使用的預設模式[setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)方法，將會認可您的每個動作。 對於多數開發人員而言，這是最容易使用的模式。  
  
 當您使用手動交易時，請確認您的程式碼可以盡快認可交易。 讓交易持續開啟會讓其他使用者無法存取資料。 例如，一個良好的程式設計作法可能是將復原呼叫放到您的 catch 區塊，並將認可呼叫放到最終的區塊。 不過，這取決於您應用程式的設計。  
  
 讓交易的大小保持越小，所建立的並行越好。 例如，如果您啟動手動交易，並在 20,000 個資料列的資料表中修改 10,000 個資料列，您將針對其他所有使用者完全封鎖一半的資料表，即使他們只在讀取資料也一樣。 將您的修改減少為 2,000 個資料列則會讓 90% 的表格可以使用。  
  
 此外，如果您的應用程式預期會發生一些封鎖問題而且需要進行逾時，請務必使用鎖定逾時設定。 您可以使用[setLockTimeout](../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)方法。 鎖定逾時的預設值為 -1，也就是說，在等待鎖定時，它會永遠封鎖。 您可以將鎖定逾時設定為 30 秒，也就是說，如果由其他連接進行封鎖，將會使封鎖的連接逾時 30 秒。  
  
## <a name="see-also"></a>另請參閱  
 [提升效能和可靠性，JDBC 驅動程式](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
