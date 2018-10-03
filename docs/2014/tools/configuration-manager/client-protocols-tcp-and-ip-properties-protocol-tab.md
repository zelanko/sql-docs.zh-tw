---
title: 用戶端通訊協定-TCP 和 IP 屬性 （通訊協定索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- configmgr-client
ms.topic: conceptual
helpviewer_keywords:
- TCP/IP [SQL Server], client protocols
- client protocols [SQL Server]
ms.assetid: d04f1bce-069c-4a02-b561-c87c3282be36
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d7686844144b43467c152907dfdff10a033005b7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165208"
---
# <a name="client-protocols---tcp-and-ip-properties-protocol-tab"></a>用戶端通訊協定 - TCP 和 IP 屬性 (通訊協定索引標籤)
  在「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」中，您可以使用 **[TCP/IP 內容]** 對話方塊中的 **[通訊協定]** 索引標籤來檢視或指定下列選項。 若要連接到其他通訊埠，請在 **[預設通訊埠]** 方塊內輸入通訊埠編號。 如需連接字串的詳細資訊，請參閱 [使用 TCP/IP 建立有效的連接字串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)。  
  
## <a name="options"></a>選項。  
 **[預設通訊埠]**  
 指定 TCP/IP 網路程式庫嘗試連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的目標執行個體時，要使用的預設通訊埠。 預設的通訊埠值為 1433。  
  
 連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的預設執行個體時，用戶端會使用這個值。 如果預設執行個體已設為接聽不同的通訊埠，請將此值變更為該通訊埠編號。  
  
 連接到具名的 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體時，用戶端會嘗試從在伺服器電腦執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser Service 取得通訊埠編號。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser Service 未執行，就必須透過這項設定提供通訊埠編號，或者以連接字串方式提供。  
  
 **已啟用**  
 可能的值為 [是] 和 [否]。  
  
 **Keep Alive**  
 此參數 (以毫秒為單位) 藉由傳送 **KEEPALIVE** 封包，來控制 TCP 嘗試驗證閒置連線是否仍完整無缺的頻率。 預設為 30000 毫秒。  
  
 **保持運作的間隔**  
 此參數 (以毫秒為單位) 可決定在收到回應之前，用以分隔 **KEEPALIVE** 重新傳輸的間隔。 預設為 1000 毫秒。  
  
## <a name="see-also"></a>另請參閱  
 [選擇網路通訊協定](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [新增別名 &#40;[別名] 索引標籤&#41;](../../../2014/tools/configuration-manager/new-alias-alias-tab.md)   
 [&#60;別名&#62;屬性&#40;別名索引標籤&#41;](../../../2014/tools/configuration-manager/alias-properties-alias-tab.md)  
  
  
