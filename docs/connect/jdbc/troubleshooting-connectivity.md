---
title: 疑難排解連線 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2dcf0e17eb4983cc9ae9cc4a01c1fe7b7f1a44a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshooting-connectivity"></a>連接性疑難排解
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]需要 TCP/IP，才能安裝並執行與您[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。 您可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]組態管理員來確認已安裝的網路程式庫通訊協定。  
  
 資料庫連接嘗試可能會因為許多因素而失敗。 這些因素如下所述：  
  
-   未啟用 TCP/IP [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，或指定的伺服器或連接埠號碼不正確。 確認[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]會接聽指定的伺服器和連接埠上的 TCP/IP。 可能會報告類似以下的例外狀況：「登入失敗。 TCP/IP 連接至主機已失敗。」 此訊息會指出下列其中一項：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 已安裝但 TCP/IP 尚未安裝做為網路通訊協定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]網路公用程式[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]，或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]適用之 Configuration Manager[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]和更新版本。  
  
    -   TCP/IP 已安裝為[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通訊協定，但它並未接聽在 JDBC 連接 URL 中指定的連接埠。 預設連接埠為 1433，但[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，可以在產品安裝，以接聽任何通訊埠設定。 請確定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通訊埠 1433年上接聽。 或者，如果已變更通訊埠，則請確定 JDBC 連接 URL 中所指定的通訊埠符合已變更的通訊埠。 如需 JDBC 連接 Url 的詳細資訊，請參閱[建立連接 URL](../../connect/jdbc/building-the-connection-url.md)。  
  
    -   JDBC 連接中指定之電腦的位址 URL 並未參考伺服器其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]會安裝並啟動。  
  
    -   用戶端與伺服器之間的 TCP/IP 網路作業[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不是可執行。 您可以檢查 TCP/IP 連接性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用 telnet。 例如，在命令提示字元中，輸入`telnet 192.168.0.0 1433`其中 192.168.0.0 為執行電腦的位址[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]而 1433年則為正在接聽的連接埠。 如果您收到訊息，指出 「 Telnet 無法連接 」 時，TCP/IP 未接聽該通訊埠[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]連線。 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]網路公用程式[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]，或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]適用之 Configuration Manager[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]版本，請確定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]設定為使用 TCP/IP 通訊埠 1433年。  
  
    -   伺服器所使用的通訊埠尚未在防火牆內開啟。 這包括伺服器所使用的通訊埠，或與具名的伺服器執行個體相關聯的選用通訊埠。  
  
-   指定的資料庫名稱不正確。 請確定您正登入到現有[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。  
  
-   使用者名稱或密碼不正確。 請確定您擁有正確的值。  
  
-   當您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證，JDBC 驅動程式會要求[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]會隨[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證，但不是預設值。 請確定您安裝或設定您的執行個體時，會包含此選項[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [診斷 JDBC 驅動程式的問題](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [使用 JDBC Driver 連接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
