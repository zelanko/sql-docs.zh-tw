---
title: 疑難排解連線能力 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ae5f65538c0303a92fdb86f71d75a556ad3f458
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840886"
---
# <a name="troubleshooting-connectivity"></a>連接性疑難排解
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 需要已安裝並執行 TCP/IP 後，才能與您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫通訊。 您可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來確認哪些網路程式庫通訊協定已安裝。  
  
 資料庫連接嘗試可能會因為許多因素而失敗。 這些因素如下所述：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未啟用 TCP/IP，或者指定的伺服器或連接埠號碼不正確。 確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在接聽指定伺服器與連接埠上的 TCP/IP。 可能會報告類似以下的例外狀況：「登入失敗。 TCP/IP 連接至主機已失敗。」 此訊息會指出下列其中一項：  
  
    -   已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但未使用 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 網路公用程式，或是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，將 TCP/IP 安裝為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的網路通訊協定。  
  
    -   TCP/IP 已安裝為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通訊協定，但未在 JDBC 連線 URL 中指定的連接埠上接聽。 預設連接埠為 1433，但可在產品安裝期間將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為在任何連接埠上接聽。 請確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正於連接埠 1433 上接聽。 或者，如果已變更通訊埠，則請確定 JDBC 連接 URL 中所指定的通訊埠符合已變更的通訊埠。 如需有關 JDBC 連接 Url 的詳細資訊，請參閱 < [Building the Connection URL](../../connect/jdbc/building-the-connection-url.md)。  
  
    -   JDBC 連線 URL 中指定的電腦位址並不是指已安裝並啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的伺服器。  
  
    -   用戶端與執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之伺服器間的 TCP/IP 網路作業無法運作。 您可使用 telnet 檢查 TCP/IP 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連線能力。 例如，在命令提示字元中鍵入 `telnet 192.168.0.0 1433`，其中 192.168.0.0 是執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦位址，而 1433 則是目前接聽所在的連接埠。 如果您收訊息，內容指出「Telnet 無法連線」，即表示 TCP/IP 沒有在該連接埠上接聽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連線。 請使用 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 網路公用程式，或是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，來確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已設定為在連接埠 1433 上使用 TCP/IP。  
  
    -   伺服器所使用的通訊埠尚未在防火牆內開啟。 這包括伺服器所使用的通訊埠，或與具名的伺服器執行個體相關聯的選用通訊埠。  
  
-   指定的資料庫名稱不正確。 請確定您正在登入現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
-   使用者名稱或密碼不正確。 請確定您擁有正確的值。  
  
-   當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，JDBC 驅動程式需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證一同安裝，這不是預設。 請確定當您安裝或設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，已包含此選項。  
  
## <a name="see-also"></a>另請參閱  
 [診斷 JDBC 驅動程式的問題](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [使用 JDBC Driver 連接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
