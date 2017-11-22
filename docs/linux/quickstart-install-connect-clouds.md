---
title: "開始使用雲端中的 SQL Server 2017 |Microsoft 文件"
description: "本快速入門教學課程會示範如何在您選擇的雲端中的 Linux 上執行 SQL Server 2017。"
author: annashres
ms.author: annashres
manager: jhubbard
ms.date: 10/25/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.openlocfilehash: 0bc304b50930f8c8de5d244ea0b606add5f24d2f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="run-the-sql-server-2017-in-the-cloud"></a>在雲端中執行 SQL Server 2017

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

在本快速入門教學課程中，您將安裝 SQL Server 2017 Red Hat Enterprise Linux (RHEL)、 SUSE Linux Enterprise Server (SLES) 或您選擇的雲端中的 Ubuntu 上。 移至[佈建 Azure 入口網站中的 Linux SQL Server 虛擬機器](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)在 Azure 中 Linux 上執行 SQL Server。

    > [!NOTE]
    > If you choose to run a paid edition of SQL Server then you need to bring your own license (BYOL)

## <a name="amazon-web-services"></a>Amazon Web Services
1.  建立 Linux AMI 至少 3.25 gb 的記憶體從 marketplace 
    * [RHEL 7.3 +](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  連接到與 AMI ssh
1.  請遵循您所選擇的 Linux distrbution 的快速入門： 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  遠端連線設定： 
    * 開啟[Amazon EC2 主控台]( https://console.aws.amazon.com/ec2/)
    * 在瀏覽窗格中，選擇 **安全性群組**。 
    * 選擇**輸入時，編輯、 加入規則**
    * 新增輸入的規則以允許 SQL Server 接聽 （預設值 TCP 通訊埠 1433年） 的連接埠上的流量

    
## <a name="digital-ocean"></a>數位 Ocean
1. 登入[控制台](https://cloud.digitalocean.com/login)按一下建立 droplet
1. 選擇 Ubuntu 16.04 droplet 至少 3.25 gb 的記憶體
1. 連接到與 droplet ssh
1. 請遵循[Ubuntu 快速入門](quickstart-install-connect-ubuntu.md)
1. 遠端連線設定：
    * 在控制台中的頂端，請遵循**網路**連結，然後選取 **防火牆**
    * 新增輸入的規則以允許 SQL Server 接聽 （預設值 TCP 通訊埠 1433年） 的連接埠上的流量
    
## <a name="google-cloud-platform"></a>Google 雲端平台
1.  在至少 3.25 gb 的記憶體從雲端啟動器建立 Linux 映像 
    * [RHEL 7.3 +](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  連接到影像的 ssh
1.  請遵循您所選擇的 Linux distrbution 的快速入門： 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  遠端連線設定： 
    * 移至[防火牆規則](https://console.cloud.google.com/networking/firewalls)
    * 新增輸入的規則以允許 SQL Server 接聽 (預設值 tcp: 1433) 的連接埠上的流量
