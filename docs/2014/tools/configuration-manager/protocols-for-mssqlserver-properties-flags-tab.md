---
title: MSSQLSERVER 屬性的通訊協定 ([旗標] 索引標籤) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- MSSQLSERVER property protocols
ms.assetid: 4d38e6e9-f95f-4e79-ae45-89f631037528
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 937485df231bcff089157bd8fee05ebd913a4ff4
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63459862"
---
# <a name="protocols-for-mssqlserver-properties-flags-tab"></a>MSSQLSERVER 的通訊協定內容 (旗標索引標籤)
  在伺服器上安裝憑證之後，您可以使用 **[MSSQLSERVER 的通訊協定內容]** 對話方塊的 **[旗標]** 索引標籤來檢視或指定通訊協定的加密，並且隱藏執行個體選項。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須重新啟動，才能啟用或停用 **[ForceEncryption]** 設定。  
  
 若要將連接加密，您應該提供具有憑證的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 。 若未安裝憑證， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在執行個體啟動時產生自我簽署憑證。 此自我簽署憑證可用來代替信任的憑證授權單位發行的憑證，但它並不提供驗證或不可否認性。  
  
> [!CAUTION]  
>  使用自我簽署憑證來加密的安全通訊端層 (SSL) 連接無法提供增強式安全性。 此方式可能遭受攔截式攻擊 (man-in-the-middle attack) 的威脅。 在實際執行環境或連接到網際網路的伺服器上，您不應該仰賴使用自我簽署憑證的 SSL。  
  
 如需有關加密的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書》中的＜將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連接加密＞。  
  
 登入過程一律加密。 當 **[ForceEncryption]** 設為 **[是]** 時，所有用戶端/伺服器通訊都會加密，且連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的用戶端必須設定為信任伺服器憑證的根授權單位。 如需詳細資訊，請參閱 「 如何：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜如何：啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的加密連接 ( 組態管理員)＞。  
  
## <a name="cluster-servers"></a>叢集伺服器  
 如果您想要對容錯移轉叢集使用加密，請務必使用容錯移轉叢集中，所有節點之虛擬伺服器的完整 DNS 名稱來安裝伺服器憑證。 例如，假設您有一個雙節點的叢集，節點的名稱分別為 "test1.*\<貴公司>*.com" 和 "test2.*\<貴公司>*.com"，而且您有一個名為 "virtsql" 的虛擬伺服器，則將會需要在兩個節點上都安裝 "virtsql.*\<貴公司>*.com" 的憑證。 接著，您可以選取 **[SQL Server 組態管理員]** 中的 **[ForceEncryption]** 核取方塊，設定要執行加密的容錯移轉叢集。  
  
## <a name="options"></a>選項。  
 **[ForceEncryption]**  
 強制通訊協定加密。 加密是一種將資料變成無法讀取的形式，使機密資訊保持機密的方法。 加密可以確保資料的安全性，即使是在傳輸處理中傳輸封包被檢視時。 若要使用通道繫結，請將 **[強制加密]** 設定為 **[開啟]** ，並在 **[進階]** 索引標籤上設定 **[擴充保護]** 。  
  
 **HideInstance**  
 防止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務將此 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體公開給嘗試利用 **[瀏覽]** 按鈕尋找執行個體的用戶端電腦。 如果是伺服器上的具名執行個體，連接時，用戶端電腦必須指定通訊協定端點資訊。 例如，連接埠編號或具名管道名稱，如 `tcp:server,5000`。 如需詳細資訊，請參閱 [Logging In to SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)。  
  
 如需詳細資訊，請參閱 「 如何：啟用加密連接到 Database Engine （SQL Server 組態管理員） 」 線上叢書 》。  
  
  
