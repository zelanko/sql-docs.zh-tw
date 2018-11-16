---
title: 在 Azure 虛擬機器上安裝 SQL Server 機器學習服務 R 和 Python |Microsoft Docs
description: R 和 Python 資料科學和機器學習服務解決方案，在 Azure 雲端中的 SQL Server 虛擬機器上執行。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e416b99c3d4597cb2fe9346819184be43cd98402
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512693"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>在 Azure 虛擬機器上安裝 SQL Server 機器學習服務 R 和 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

您可以在 Azure 中，排除安裝和設定工作在 SQL Server 虛擬機器上，使用機器學習服務安裝 R 和 Python 整合。 一旦部署虛擬機器的功能都可供使用。
 
如需逐步指示，請參閱 <<c0> [ 如何佈建 Windows SQL Server 虛擬機器在 Azure 入口網站中](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision)。

[設定 SQL server 設定](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#4-configure-sql-server-settings)步驟是，您將機器學習服務加入您的執行個體。

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>解除封鎖防火牆

根據預設，Azure 虛擬機器上的防火牆會包含規則，封鎖網路本機使用者帳戶的存取權。

您必須停用此規則，確保您可以存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從遠端資料科學用戶端的執行個體。  否則，您的機器學習程式碼無法在使用虛擬機器的工作區的計算內容中執行。

若要啟用從遠端資料科學用戶端存取：

1. 在虛擬機器上，開啟 [具有進階安全性的 Windows 防火牆]。
2. 選取 [輸出規則]
3. 停用下列規則︰
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>針對遠端用戶端啟用 ODBC 回呼

如果您預期呼叫伺服器的用戶端將會需要發出 ODBC 查詢做為其機器學習服務解決方案的一部分，您必須確定 Launchpad 可代表遠端用戶端的 ODBC 呼叫。 

若要這樣做，您必須允許 Launchpad 所使用的 SQL 背景工作帳戶登入執行個體。 如需詳細資訊，請參閱 <<c0> [ 為資料庫使用者的新增 SQLRUserGroup](../security/add-sqlrusergroup-to-database.md)。

<a name="network"></a>

## <a name="add-network-protocols"></a>新增網路通訊協定

+ 啟用具名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會針對用戶端和伺服器電腦之間的連線，以及部分內部連線使用「具名管道」通訊協定。 如果未啟用具名管道，您必須同時在 Azure 虛擬機器以及連線 到伺服器的任何資料科學用戶端上，安裝具名管道並將它啟用。
  
+ 啟用 TCP/IP

  TCP/IP 是為了使用回送連接。 如果您收到錯誤 「 DBNETLIB;SQL Server 不存在或拒絕存取，"請在支援的執行個體的虛擬機器上啟用 TCP/IP。