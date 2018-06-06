---
title: 預設 SQL Server 網路通訊協定組態 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server], default settings
- default protocols, after install
ms.assetid: 635ea361-a797-4971-bd05-e3415862bc5c
caps.latest.revision: 4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 93a6669821de69a5dff3a7ab58ff35cf3f24fee8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32866615"
---
# <a name="default-sql-server-network-protocol-configuration"></a>預設 SQL Server 網路通訊協定組態
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
為了加強安全性， [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 會為新安裝停用網路連接性。 如果您正在使用 Enterprise、Standard、Evaluation 或 Workgroup Edition 或是 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的舊版安裝仍然存在，就不會停用使用 TCP/IP 的網路連接。 所有的安裝都會啟用共用記憶體通訊協定，以允許本機連接到伺服器。 視安裝條件和安裝選項而定， [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser 服務有可能會停止。

使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 組態管理員的 [ [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 網路組態] 節點，在安裝後設定網路通訊協定。 使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 組態管理員的 [ [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 服務] 節點，設定 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser 服務自動啟動。 如需詳細資訊，請參閱 [啟用或停用伺服器網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。


## <a name="default-configuration"></a>預設組態

下表描述安裝後的組態。

版本 | 有新安裝還是舊版安裝存在 | 共用記憶體 | TCP/IP    | 具名管道
| -------- | -- | -- | -- | --  |  
Enterprise  | 新安裝  | 已啟用   | 已啟用   | 針對網路連接停用。
Standard    | 新安裝  | 已啟用   | 已啟用   | 針對網路連接停用。
Web | 新安裝  | 已啟用   | 已啟用   | 針對網路連接停用。
Developer   | 新安裝  | 已啟用   | 已停用  | 針對網路連接停用。
Evaluation  | 新安裝  | 已啟用   | 已啟用   | 針對網路連接停用。
SQL Server Express  | 新安裝  | 已啟用   | 已停用  | 針對網路連接停用。
所有版本    | 存在舊版安裝，但未升級   | 與新安裝相同  | 與新安裝相同  | 與新安裝相同
所有版本    | UPGRADE   | 已啟用   | 保留舊版安裝的設定。    | 保留舊版安裝的設定。


>[!NOTE]
> 如果執行個體是在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 容錯移轉叢集上執行，則會接聽您在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝期間為 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 選取之每個 IP 位址的這些連接埠。
 
>[!NOTE]
> 在使用命令提示字元引數安裝 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 時，您可以使用 `TCPENABLED` 和 `NPENABLED` 參數來指定要啟用的通訊協定。 如需詳細資訊，請參閱 [從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。

## <a name="creating-a-connection-string"></a>建立連接字串

如需連接字串範例，請參閱下列主題︰
* [使用共用記憶體通訊協定建立有效的連接字串](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
* [Creating a Valid Connection String Using TCP IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)



## <a name="includessnoversionmdincludesssnoversion-mdmd-browser-settings"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 瀏覽器設定

安裝過程中，可以將 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser 服務設定為自動啟動。 預設值為在下列狀況成立時，此服務才會自動啟動：

* 升級安裝時。
* 與另一個 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體並存安裝時。
* 在叢集上安裝時。
* 安裝 Database Engine 的具名執行個體並包括所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Express 執行個體時。
* 安裝 Analysis Services 的具名執行個體時。

## <a name="see-also"></a>另請參閱

[安裝 SQL Server 2016 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)

[介面區組態](../../relational-databases/security/surface-area-configuration.md)  



