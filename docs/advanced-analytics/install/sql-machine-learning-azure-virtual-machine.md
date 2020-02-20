---
title: 在 Azure 虛擬機器上安裝
description: 在 Azure 雲端中的虛擬機器上，搭配 SQL Server 機器學習服務執行 Python 與 R 資料科學與機器學習解決方案。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d81237f67c82fd7cc8b9259fcd7a0202ffb7fd4b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75776587"
---
# <a name="install-sql-server-machine-learning-services-with-python-and-r-on-an-azure-virtual-machine"></a>在 Azure 虛擬機器上搭配 Python 與 R 安裝 SQL Server 機器學習服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

了解如何在 Azure 中的虛擬機器上，搭配 SQL Server 機器學習服務安裝 Python 與 R。 這樣可減少機器學習服務的安裝及設定工作。

請遵循下列步驟：

1. 在 Azure 中佈建 SQL Server 虛擬機器
1. 解除封鎖防火牆
1. 針對遠端用戶端啟用 ODBC 回呼
1. 新增網路通訊協定

## <a name="provision-sql-server-virtual-machine-in-azure"></a>在 Azure 中佈建 SQL Server 虛擬機器

如需逐步指示，請參閱[如何在 Azure 入口網站中佈建 Windows SQL Server 虛擬機器](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision) \(部分機器翻譯\)。 

[設定 SQL Server 設定](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) \(部分機器翻譯\) 步驟是您將機器學習服務新增到執行個體的步驟。

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>解除封鎖防火牆

根據預設，Azure 虛擬機器上的防火牆包含會封鎖本機使用者帳戶之網路存取權的規則。

您必停用此規則以確保您可以從遠端資料科學用戶端存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  否則，您的機器學習程式碼無法在使用虛擬機器工作區的計算內容中執行。

啟用遠端資料科學用戶端的存取權：

1. 在虛擬機器上，開啟 [具有進階安全性的 Windows 防火牆]。
2. 選取 [輸出規則] 
3. 停用下列規則︰
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>針對遠端用戶端啟用 ODBC 回呼

如果您預期呼叫伺服器的用戶端將需要發出 ODBC 查詢做為其機器學習解決方案的一部分，您必須確定 Launchpad 可代表遠端用戶端進行 ODBC 呼叫。 

若要這樣做，您必須允許 Launchpad 所使用的 SQL 背景工作帳戶登入執行個體。 如需詳細資訊，請參閱[將 SQLRUserGroup 新增為資料庫使用者](../security/create-a-login-for-sqlrusergroup.md)。

<a name="network"></a>

## <a name="add-network-protocols"></a>新增網路通訊協定

+ 啟用具名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會針對用戶端和伺服器電腦之間的連線，以及部分內部連線使用「具名管道」通訊協定。 如果未啟用具名管道，您必須同時在 Azure 虛擬機器以及連線 到伺服器的任何資料科學用戶端上，安裝具名管道並將它啟用。
  
+ 啟用 TCP/IP

  TCP/IP 是回送連線的必要項。 若您遇到錯誤「DBNETLIB; 不存在或存取遭拒」，請在支援執行個體的虛擬機器上啟用 TCP/IP。