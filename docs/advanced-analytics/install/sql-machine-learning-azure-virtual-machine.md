---
title: 在 Azure 虛擬機器上安裝 R 語言和 Python 功能
description: 在 Azure 雲端中的 SQL Server 虛擬機器上執行 R 和 Python 資料科學和機器學習服務解決方案。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6f034f3a766e4f82bd1bcfd182f4eee285f7f829
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345039"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>在 Azure 虛擬機器上使用 R 和 Python 安裝 SQL Server Machine Learning 服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

您可以在 Azure 中的 SQL Server 虛擬機器上安裝 R 和 Python 與 Machine Learning 服務的整合, 以排除安裝和設定工作。 部署虛擬機器之後, 即可使用這些功能。
 
如需逐步指示, 請參閱[如何在 Azure 入口網站中布建 Windows SQL Server 虛擬機器](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision)。

[[設定 SQL server 設定](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings)] 步驟可讓您將機器學習新增至實例。

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>解除封鎖防火牆

根據預設, Azure 虛擬機器上的防火牆包含封鎖本機使用者帳戶網路存取的規則。

您必須停用此規則, 以確保您可以從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遠端資料科學用戶端存取實例。  否則, 您的機器學習服務程式代碼無法在使用虛擬機器工作區的計算內容中執行。

若要啟用遠端資料科學用戶端的存取:

1. 在虛擬機器上，開啟 [具有進階安全性的 Windows 防火牆]。
2. 選取 [輸出規則] 
3. 停用下列規則︰
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>針對遠端用戶端啟用 ODBC 回呼

如果您預期呼叫伺服器的用戶端必須發出 ODBC 查詢作為其機器學習解決方案的一部分, 則您必須確定啟動列會代表遠端用戶端進行 ODBC 呼叫。 

若要這樣做，您必須允許 Launchpad 所使用的 SQL 背景工作帳戶登入執行個體。 如需詳細資訊, 請參閱[將 SQLRUserGroup 新增為資料庫使用者](../security/create-a-login-for-sqlrusergroup.md)。

<a name="network"></a>

## <a name="add-network-protocols"></a>新增網路通訊協定

+ 啟用具名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會針對用戶端和伺服器電腦之間的連線，以及部分內部連線使用「具名管道」通訊協定。 如果未啟用具名管道，您必須同時在 Azure 虛擬機器以及連線 到伺服器的任何資料科學用戶端上，安裝具名管道並將它啟用。
  
+ 啟用 TCP/IP

  回送連接需要 TCP/IP。 如果您收到錯誤「DBNETLIB;SQL Server 不存在或拒絕存取」, 請在支援實例的虛擬機器上啟用 TCP/IP。