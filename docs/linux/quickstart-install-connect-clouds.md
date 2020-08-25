---
title: 在雲端中開始使用 Linux 上的 SQL Server
titleSuffix: SQL Server
description: 了解如何在所選擇雲端中的 Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES) 或 Ubuntu 上安裝 SQL Server。
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: d40072ea8b347001feba5d74e6e08c8c4c8ae340
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2020
ms.locfileid: "88089024"
---
# <a name="quickstart-run-sql-server-in-the-cloud"></a>快速入門：在雲端中執行 SQL Server
[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

在本快速入門中，您會在所選擇的雲端 Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES) 或 Ubuntu 上安裝 SQL Server。 請前往 [Provision a Linux SQL Server virtual machine in the Azure portal](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json) (在 Azure 入口網站中佈建 Linux SQL Server 虛擬機器)，了解如何在 Azure 中執行 Linux 上的 SQL Server。

> [!NOTE]
> 如果您選擇執行 SQL Server 的付費版本，則需要自備授權 (BYOL)。

## <a name="amazon-web-services"></a>Amazon Web Services
1.  從 Marketplace 建立至少有 2 GB 記憶體的 Linux AMI 
    * [RHEL 7.3+](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2+](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  使用 ssh 連線到 AMI
1.  遵循 Linux 發行版本的快速入門，選擇： 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  設定遠端連線： 
    * 開啟 [Amazon EC2 主控台]( https://console.aws.amazon.com/ec2/)
    * 在瀏覽窗格中，選擇 [Security Groups] \(安全性群組\)  。 
    * 選擇 [Inbound] \(輸入\)、[Edit] \(編輯\)、[Add Rule] \(新增規則\) 
    * 新增輸入規則，允許 SQL Server 所接聽通訊埠上的流量 (預設 TCP 通訊埠 1433)

    
## <a name="digital-ocean"></a>Digital Ocean
1. 登入[控制台](https://cloud.digitalocean.com/login)，然後按一下 [create a droplet] \(建立 Droplet\)
1. 選擇至少有 2 GB 記憶體的 Ubuntu 16.04 Droplet
1. 使用 ssh 連線到 Droplet
1. 遵循 [Ubuntu 快速入門](quickstart-install-connect-ubuntu.md)
1. 設定遠端連線：
    * 在控制台頂端，遵循 [Networking] \(網路\)  連結，然後選取 [Firewalls] \(防火牆\) 
    * 新增輸入規則，允許 SQL Server 所接聽通訊埠上的流量 (預設 TCP 通訊埠 1433)
    
## <a name="google-cloud-platform"></a>Google Cloud Platform
1.  從 Cloud Launcher 建立至少有 2 GB 記憶體的 Linux 映像 
    * [RHEL 7.3+](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP4](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  使用 ssh 連線到映像
1.  遵循 Linux 發行版本的快速入門，選擇： 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  設定遠端連線： 
    * 前往 [Firewall Rules](https://console.cloud.google.com/networking/firewalls) (防火牆規則)
    * 新增輸入規則，允許 SQL Server 所接聽通訊埠上的流量 (預設 TCP：1433)
