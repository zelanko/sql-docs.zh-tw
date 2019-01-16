---
title: 開始使用雲端中的 SQL Server （在 Linux 上）
titleSuffix: SQL Server
description: 本快速入門示範如何在您選擇的雲端中的 Linux 上執行 SQL Server。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/25/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 77e818109424b5f0d9dea3b495da4e927c506366
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/15/2019
ms.locfileid: "54299235"
---
# <a name="quickstart-run-sql-server-in-the-cloud"></a>快速入門：在雲端中執行 SQL Server

  > [!div class="nextstepaction"]
  > [請分享您對 SQL Docs 目錄內容的意見 ！](https://aka.ms/sqldocsurvey)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在本快速入門中，您將 Red Hat Enterprise Linux (RHEL)、 SUSE Linux Enterprise Server (SLES) 或您選擇的雲端中的 Ubuntu 上安裝 SQL Server。 移至[佈建 Linux SQL Server 虛擬機器在 Azure 入口網站中](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)在 Azure 中的 Linux 上執行 SQL Server。

> [!NOTE]
> 如果您選擇執行 SQL Server 的付費的版本，您就需要自備授權 (BYOL)。

## <a name="amazon-web-services"></a>Amazon Web Services
1.  使用至少 2 GB 的記憶體從 marketplace 建立 Linux AMI 
    * [RHEL 7.3+](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Ssh 連線到與 AMI
1.  請依照下列快速入門中，您所選擇的 Linux 散發套件： 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  設定遠端連線： 
    * 開啟[Amazon EC2 主控台]( https://console.aws.amazon.com/ec2/)
    * 在 [導覽] 窗格中，選擇**安全性群組**。 
    * 選擇**輸入、 編輯、 新增規則**
    * 新增輸入的規則以允許 SQL Server 接聽 （預設值 TCP 通訊埠 1433年） 的連接埠上的流量

    
## <a name="digital-ocean"></a>Digital Ocean
1. 登入[控制台中](https://cloud.digitalocean.com/login)然後按一下 建立 droplet
1. 選擇 Ubuntu 16.04 droplet 至少 2 gb 的記憶體
1. Ssh 連線到與 droplet
1. 請依照下列[Ubuntu 快速入門](quickstart-install-connect-ubuntu.md)
1. 設定遠端連線：
    * 在控制台中的頂端，請遵循**Networking**連結，然後選取 **防火牆**
    * 新增輸入的規則以允許 SQL Server 接聽 （預設值 TCP 通訊埠 1433年） 的連接埠上的流量
    
## <a name="google-cloud-platform"></a>Google 雲端平台
1.  使用至少 2 GB 的記憶體從雲端啟動程式中建立的 Linux 映像 
    * [RHEL 7.3+](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Ssh 連線到具有的映像
1.  請依照下列快速入門中，您所選擇的 Linux 散發套件： 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  設定遠端連線： 
    * 移至[防火牆規則](https://console.cloud.google.com/networking/firewalls)
    * 新增輸入的規則以允許 SQL Server 所接聽的連接埠上的流量 (預設值 tcp:1433)
