---
title: TCP/IP 屬性 (IP 位址索引標籤)
ms.custom: seo-lt-2019
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], listening on
- listening [SQL Server], on ports
ms.assetid: 4c17ed45-9da7-4bec-bce6-970109fe7365
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f1afdb9d25d599f32b2efb9d5339ef4afffd6f31
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307559"
---
# <a name="tcpip-properties-ip-addresses-tab"></a>TCP/IP 屬性 (IP 位址索引標籤)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  您可以使用 **[TCP/IP 屬性 (IP 位址索引標籤)]** 對話方塊，設定特定 IP 位址的 TCP/IP 通訊協定選項。 您只能透過選取 **[IPAll]** ，一次設定所有位址的 **[TCP 動態通訊埠]** 和 **[TCP 通訊埠]** 。  
  
 重新啟動 SQL Server 之後，變更才會生效。 如需啟動和停止 SQL Server Browser 服務的資訊，請參閱 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
## <a name="static-vs-dynamic-ports"></a>靜態與動態通訊埠  
 預設的 SQL Server 執行個體使用通訊埠 1433 接聽內送連接。 為了安全上的理由或因為用戶端應用程式的需求，可以變更此通訊埠。 根據預設，具名執行個體 (包括 SQL Server Express) 設定為接聽動態通訊埠。 若要設定靜態通訊埠，請將 **[TCP 動態通訊埠]** 方塊保留空白，並於 **[TCP 通訊埠]** 方塊中提供可用的通訊埠編號。 如需有關在防火牆中開啟通訊埠的詳細資訊，請參閱線上叢書中的＜將 Windows 防火牆設定成允許 SQL Server 存取＞。  
  
## <a name="dynamic-ports"></a>動態通訊埠  
 當 SQL Server 的執行個體設為接聽動態通訊埠，就會在啟動時檢查作業系統是否有可用的通訊埠，並為該通訊埠開啟一個端點。 內送連接必須指定要連接的通訊埠編號。 因為 SQL Server 每次啟動時通訊埠編號都會變更，所以 SQL Server 會提供 SQL Server Browser 服務以監視通訊埠，並將內送連接導向該執行個體目前的通訊埠。 使用動態通訊埠時，透過防火牆連接 SQL Server 將變得非常複雜，因為 SQL Server 重新啟動時通訊埠編號可能會變更，因此需要變更防火牆設定。 若要避免透過防火牆連接時發生問題，請將 SQL Server 設定為使用靜態通訊埠。  
  
## <a name="options"></a>選項。  
 **使用中**  
 指出電腦上的 IP 位址為使用中狀態。 不適用於 **[IPAll]** 。  
  
 **已啟用**  
 如果 **[TCP/IP 屬性 (通訊協定索引標籤)]** 上的 **[全部接聽]** 屬性設為 **[否]** ，此屬性便會指出 SQL Server 是否正在接聽該 IP 位址。 如果 **[TCP/IP 屬性 (通訊協定索引標籤)]** 上的 **[全部接聽]** 屬性設為 **[是]** ，則會忽略此屬性。 不適用於 **[IPAll]** 。  
  
 **IP 位址**  
 檢視或變更此連線使用的 IP 位址。 列出電腦使用的 IP 位址以及 IP 回送位址 127.0.0.1。 不適用於 **[IPAll]** 。 IP 位址可以採用 IPv4 或 IPv6 其中一種格式。  
  
 **[IPAll]**  
 如果未啟用動態通訊埠，就會空白。 若要使用動態通訊埠，請設為 0。  
  
 若為 **[IPAll]** ，則顯示使用之動態通訊埠的通訊埠編號。  
  
 **[TCP 動態通訊埠]**  
 檢視或變更 SQL Server 接聽的通訊埠。 根據預設，SQL Server 的預設執行個體會接聽通訊埠 1433。  
  
 資料庫引擎可以在同一個 IP 位址接聽多個通訊埠，方法是使用逗號隔開通訊埠 (例如，1433,1500,1501)。 此欄位最長不可超過 2047 個字元。  
  
 若要設定單一 IP 位址接聽多個通訊埠，還必須在 [TCP/IP 屬性] 對話方塊的 [通訊協定] 索引標籤上，將 [全部接聽] 參數設為 [否]。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜如何：設定 Database Engine 接聽多個 TCP 通訊埠＞。  
  
## <a name="adding-or-removing-ip-addresses"></a>新增或移除 IP 位址  
 SQL Server 組態管理員顯示 SQL Server 安裝後可用的 IP 位址。 加入或移除網路卡時、動態指派的 IP 位址過期時、重新設定網路結構時，或是電腦的實際位置有變化時 (例如，膝上型電腦在不同的大樓連接到網路)，可用的 IP 位址都會有變動。 若要變更 IP 位址，請編輯 [IP 位址]  方塊，然後重新啟動 SQL Server。  
  
## <a name="additional-topics-in-books-online"></a>線上叢書中的其他主題  
 搜尋 MSDN 中的主題，例如 **設定伺服器接聽特定 TCP 通訊埠 (SQL Server 組態管理員)** 和 **設定 Database Engine 接聽多個 TCP 通訊埠**。  
  
## <a name="see-also"></a>另請參閱  
 [選擇網路通訊協定](https://msdn.microsoft.com/library/ms187892(v=sql.120).aspx)   
 [使用 TCP IP 建立有效的連接字串](creating-a-valid-connection-string-using-tcp-ip.md)   
 [SQL Server Browser 服務](sql-server-browser-service.md)  
  
  
