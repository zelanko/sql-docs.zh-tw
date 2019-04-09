---
title: SSIS 服務的存取設定 Windows 防火牆 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], firewalls
- Windows Firewall [Integration Services]
- unauthorized access [Integration Services]
- Integration Services service, firewalls
- firewall systems [Integration Services]
- SQL Server Integration Services, firewalls
- SSIS, firewalls
ms.assetid: 39975cf2-c351-4205-8c39-27a0fadfb010
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c40d0003211c0446982f70a9c7a00c1f189808b6
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241897"
---
# <a name="configure-a-windows-firewall-for-access-to-the-ssis-service"></a>針對 SSIS 服務的存取設定 Windows 防火牆
    
> [!IMPORTANT]  
>  本主題會討論 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務，即用於管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支援此服務能與舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]回溯相容。 從 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]開始，您可以管理 Integration Services 伺服器上的物件，例如封裝。  
  
 Windows 防火牆系統有助於防止未經授權的使用者透過網路連接來存取電腦資源。 若要透過此防火牆存取 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ，必須設定防火牆來啟用存取。  
  
> [!IMPORTANT]  
>  若要管理儲存在遠端伺服器上的封裝，您不必連接到該遠端伺服器上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務執行個體， 而是要編輯 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務的組態檔，好讓 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 顯示儲存在遠端伺服器上的封裝。 如需詳細資訊，請參閱 [設定 Integration Services 服務 &#40;SSIS 服務&#41;](configuring-the-integration-services-service-ssis-service.md)回溯相容。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務使用 DCOM 通訊協定。 如需有關 DCOM 通訊協定如何穿越防火牆運作的詳細資訊，請參閱文章中，「[搭配防火牆使用 COM](https://manualzz.com/doc/19762578/using-distributed-com-with-firewalls-by-michael-nelson-in...)"。  
  
 有許多防火牆系統可用。 如果您是執行 Windows 防火牆以外的其他防火牆，請參閱該防火牆的文件以獲取您正在使用之系統的特定資訊。  
  
 如果防火牆支援應用程式層級篩選，您可以使用 Windows 提供的使用者介面，指定允許穿越防火牆的例外狀況，例如程式和服務。 否則，您必須設定 DCOM 使用有限的一組 TCP 通訊埠。 上一段落提供的 Microsoft 網站連結包含有關如何指定所要使用之 TCP 通訊埠的資訊。  
  
 Integration Services 服務使用通訊埠 135，且無法變更。 您必須開啟 TCP 通訊埠 135 供服務控制管理員 (SCM) 存取。 SCM 會執行工作，例如啟動和停止 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務，以及將控制要求傳送至執行中服務。  
  
 下一節內容為適用於 Windows 防火牆的特定資訊。 您可以在命令提示字元下執行命令，或在 Windows 防火牆對話方塊中設定屬性，來設定 Windows 防火牆系統。  
  
 如需預設 Windows 防火牆設定的詳細資訊，以及影響 Database Engine、Analysis Services、Reporting Services 和 Integration Services 之 TCP 通訊埠的描述，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
## <a name="configuring-a-windowsfirewall"></a>設定 Windows 防火牆  
 您可以使用下列命令來開啟 TCP 通訊埠 135，將 MsDtsSrvr.exe 加入至例外狀況清單，並指定防火牆的不封鎖範圍。  
  
#### <a name="to-configure-a-windowsfirewall-using-the-command-prompt-window"></a>若要使用命令提示字元視窗設定 Windows 防火牆  
  
1.  執行命令： `netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET`  
  
2.  執行命令： `netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET`  
  
    > [!NOTE]  
    >  若要為所有電腦以及網際網路上的電腦開啟防火牆，請以 scope=ALL 取代 scope=SUBNET。  
  
 下列程序描述如何使用 Windows 使用者介面來開啟 TCP 通訊埠 135，將 MsDtsSrvr.exe 加入例外狀況清單中，並指定防火牆的不封鎖範圍。  
  
#### <a name="to-configure-a-firewall-using-the-windowsfirewall-dialog-box"></a>若要使用 Windows 防火牆對話方塊設定防火牆  
  
1.  在 [控制台] 中按兩下 [Windows 防火牆]。  
  
2.  在 **[Windows 防火牆]** 對話方塊中，按一下 **[例外狀況]** 索引標籤，然後再按一下 **[加入程式]**。  
  
3.  在 [新增程式] 對話方塊中，按一下 [瀏覽] 巡覽至 Program Files\Microsoft SQL Server\100\DTS\Binn 資料夾，然後按一下 MsDtsSrvr.exe，再按一下 [開啟]。 按一下 **[確定]** 以關閉 **[新增程式]** 對話方塊。  
  
4.  在 **[例外狀況]** 索引標籤上，按一下 **[新增連接埠]**。  
  
5.  在 [新增連接埠] 對話方塊的 [名稱] 方塊中，輸入 **RPC(TCP/135)** 或其他描述性名稱，在 [連接埠編號] 方塊中輸入 **135**，然後選取 [TCP]。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務會一直使用通訊埠 135。 您無法指定不同的通訊埠。  
  
6.  在 **[新增連接埠]** 對話方塊中，可以選擇性地按一下 **[變更範圍]** 以修改預設範圍。  
  
7.  在 [變更範圍] 對話方塊中，選取 [只有我的網路 (子網路)] 或輸入自訂清單，然後按一下 [確定]。  
  
8.  若要關閉 **[新增連接埠]** 對話方塊，請按一下 **[確定]**。  
  
9. 若要關閉 **[Windows 防火牆]** 對話方塊，請按一下 **[確定]**。  
  
    > [!NOTE]  
    >  此程序是使用 [控制台] 中的 **[Windows 防火牆]** 項目設定 Windows 防火牆。 **[Windows 防火牆]** 項目只會針對目前網路位置設定檔來設定防火牆。 但若要設定 Windows 防火牆，您也可以使用 **netsh** 命令列工具或是 [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console (MMC) 嵌入式管理單元，名為「具有進階安全性的 Windows 防火牆」。 如需這些工具的詳細資訊，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Integration Services 服務 &#40;SSIS 服務&#41;](service/integration-services-service-ssis-service.md)   
 [Integration Services 服務 &#40;SSIS 服務&#41;](service/integration-services-service-ssis-service.md)  
  
  
