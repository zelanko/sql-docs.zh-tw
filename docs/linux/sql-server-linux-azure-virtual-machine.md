---
title: "佈建的 Linux SQL Server 在 Azure 中 VM |Microsoft 文件"
description: "本教學課程會示範如何在 Azure 中建立 Linux SQL Server 2017 虛擬機器。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 222e23b2-51e7-429b-b8e5-61e0ebe7df9b
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 0470622b0fe5a8835213617a4fc2e8c74f674873
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-linux-sql-server-2017-virtual-machine-with-the-azure-portal"></a>使用 Azure 入口網站建立 Linux SQL Server 2017 虛擬機器

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

Azure 會提供已安裝的 SQL Server 2017 RC2 的 Linux 虛擬機器映像。 本主題提供簡短的逐步解說如何使用 Azure 入口網站來建立 Linux SQL Server 虛擬機器。 

## <a name="create-a-linux-vm-with-sql-server-installed"></a>建立 Linux VM，SQL server 安裝

開啟[Azure 入口網站](https://portal.azure.com/)。

1. 按一下**新增**左側。

1. 在**新增**刀鋒視窗中，按一下 **計算**。

1. 按一下**看到所有**旁**功能的應用程式**標題。

   ![請參閱所有 VM 映像](./media/sql-server-linux-azure-virtual-machine/azure-compute-blade.png)

1. 在 [搜尋] 方塊中，輸入**SQL Server 2017**，然後按**Enter**開始搜尋。

    ![SQL Server 2017 VM 映像的搜尋篩選器](./media/sql-server-linux-azure-virtual-machine/searchfilter.png)

    > [!TIP]
    > 此篩選會顯示可用的 Linux 虛擬機器映像的 SQL Server 2017。 經過一段時間，將會列出其他支援的 Linux 散發版本的 SQL Server 2017 映像。 您也可以按一下這個[連結](https://ms.portal.azure.com/#blade/Microsoft_Azure_Marketplace/GalleryFeaturedMenuItemBlade/selectedMenuItemId/home/searchQuery/sql%20server%202017)，直接移至搜尋結果中的 SQL Server 2017。 

1. 從搜尋結果中選取的 SQL Server 2017 映像。

1. 按一下 **[建立]**。

1. 在**基本概念**刀鋒視窗中，填滿 Linux VM 的詳細資料。 

    ![基本概念刀鋒視窗](./media/sql-server-linux-azure-virtual-machine/basics.png)

    > [!Note]
    > 您可以選擇使用 SSH 公開金鑰或密碼進行驗證。 SSH 是更安全。 如需有關如何產生 SSH 金鑰的指示，請參閱[建立 SSH 金鑰在 Linux 和 Mac 上適用於在 Azure 中的 Linux Vm](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-mac-create-ssh-keys)。 

1. 按一下 **[確定]**。

1. 在**大小**刀鋒視窗中，選擇 機器大小。 開發和測試的功能，我們建議的 VM 大小**DS2**或更高版本。 基於效能測試，使用**DS13**或更高版本。

    ![選擇 VM 大小](./media/sql-server-linux-azure-virtual-machine/vmsizes.png)

    若要查看其他大小，請選取**檢視所有**。 如需 VM 機器大小的詳細資訊，請參閱[Linux VM 大小](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes)。

1. 按一下 [選取]。

1. 在**設定**刀鋒視窗中，您可以對設定進行變更或保留預設設定。

1. 按一下 **[確定]**。

1. 在**摘要**頁面上，按一下**確定**來建立 VM。

> [!NOTE]
> Azure VM 中預先設定防火牆，以開啟 遠端連接的 SQL Server 連接埠 1433年。 但若要從遠端連接，您也需要加入網路安全性群組規則下, 一節中所述。

## <a id="remote"></a>遠端連線設定

若要能夠從遠端連線到 Azure VM 上的 SQL Server，您必須設定的輸入的規則上的網路安全性群組。 此規則可讓 SQL Server 接聽 （預設值 1433年） 的連接埠上的流量。 下列步驟示範如何使用 Azure 入口網站進行此步驟。 

1. 在入口網站中，選取**虛擬機器**，然後選取 SQL Server VM。

1. 在屬性清單中，選取**網路介面**。

1. 然後選取您的 VM 網路介面。

    ![網路介面](./media/sql-server-linux-azure-virtual-machine/networkinterfaces.png)

1. 按一下 網路安全性的群組連結。

    ![網路安全性群組](./media/sql-server-linux-azure-virtual-machine/networksecuritygroup.png)

1. 內容中的網路安全性群組，選**輸入安全性規則**。

1. 按一下**+ 加** 按鈕。

1. 提供的 「 SQLServerRemoteConnections 」 的名稱。

1. 在**服務**清單中，選取**MS SQL**。

    ![MS SQL 安全性群組規則](./media/sql-server-linux-azure-virtual-machine/sqlnsgrule.png)

1. 按一下**確定**vm 儲存規則。

## <a id="connect"></a>連接至 Linux VM

如果您已經使用 BASH 殼層，連接到 Azure VM 使用**ssh**命令。 在下列命令，將 VM 使用者名稱和連接到您的 Linux VM 的 IP 位址。

```bash
ssh -l AzureAdmin 100.55.555.555
```

您可以在 Azure 入口網站中找到您的 VM 的 IP 位址。

![在 Azure 入口網站的 IP 位址](./media/sql-server-linux-azure-virtual-machine/vmproperties.png)

如果您在 Windows 上執行，而且沒有 BASH 殼層，您可以安裝的 SSH 用戶端，例如 PuTTY。

1. [下載並安裝 PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。

1. 執行 PuTTY。

1. 在 PuTTY 組態畫面中輸入 VM 的公用 IP 位址。

1. 按一下 [開啟]，並輸入您的使用者名稱和密碼提示。

如需有關如何連接至 Linux Vm 的詳細資訊，請參閱[使用入口網站在 Azure 上建立 Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-portal#ssh-to-the-vm)。

## <a name="configure-sql-server"></a>設定 SQL Server

1. 連接到您的 Linux VM 之後，開啟終端機的新命令。

1. 設定 SQL Server 使用下列命令。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup 
   ```

   接受授權並輸入系統管理員帳戶的密碼。 您可以啟動伺服器，當系統提示您。

1. （選擇性）[安裝 SQL Server 工具](sql-server-linux-setup-tools.md)。

## <a name="next-steps"></a>後續的步驟

既然您已在 Azure 中的 SQL Server 2017 虛擬機器，您可以在本機與連接**sqlcmd**執行 TRANSACT-SQL 查詢。

如果您設定遠端 SQL Server 連線的 Azure VM，您也應該能夠從遠端連線。 如需從遠端的 Windows 電腦連接到 SQL Server on Linux 的範例，請參閱[使用 SSMS 連接到 SQL Server on Linux 的 Windows 上](sql-server-linux-develop-use-ssms.md)。

多個一般 Azure 中 Linux 虛擬機器的詳細資訊，請參閱[Linux 虛擬機器文件](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/)。

