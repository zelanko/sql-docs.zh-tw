---
title: Attunity Oracle 異動資料擷取服務 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 22ec8a5c-9550-4d38-8a4a-485ec3e53ea8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 78be5b59dd2397ef361a981219989d27d88b5ae2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294821"
---
# <a name="change-data-capture-service-for-oracle-by-attunity"></a>Attunity Oracle 異動資料擷取服務

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Oracle CDC 服務是一種 Windows 服務，可掃描 Oracle 交易記錄，並將相關 Oracle 資料表的變更擷取到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 變更資料表中。 用來儲存從 Oracle 擷取之變更的 SQL 變更資料表與原生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 異動資料擷取功能中所使用的變更資料表類型相同。 如此一來，取用這些變更就像取用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫變更一樣輕鬆。  
  
## <a name="installation"></a>安裝  

適用於 Microsoft SQL Server 2016 的 Microsoft Change Data Capture Designer and Service for Oracle by Attunity 是 SQL Server 2016 Feature Pack 的一部分。 從 [SQL Server 2016 Feature Pack 網頁](https://go.microsoft.com/fwlink/?LinkId=746297)下載 Feature Pack 的元件。
  
 Oracle CDC 服務可以安裝在任何支援的 Windows 電腦上，該電腦可存取正在擷取的來源 Oracle 資料庫以及目標 CDC 資料庫所在的目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 CDC 服務不需要 Oracle 資料庫或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的本機安裝，而只需要其支援的用戶端。 如需有關要在何處安裝必要資料庫元件的詳細資訊，請參閱本主題的＜ **資料庫必要條件** ＞。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 服務的安裝會將服務組態 UI 和服務程式放在選取的位置。 Oracle CDC 服務是使用 Oracle CDC 服務組態主控台所單獨設定。 如需有關設定 Oracle CDC 服務的詳細資訊，請參閱＜ [Attunity 的 Oracle 變更資料擷取 (CDC) 服務 F1 說明](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-f1-help.md)＞。  
  
 Oracle CDC 服務可以安裝在任何支援的 Windows 電腦上，該電腦上已安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client；此服務不需要安裝在目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝所在的相同電腦上。  
  
## <a name="supported-windows-environments"></a>支援的 Windows 環境  
 Attunity Oracle Change Data Capture (CDC) 服務可在以下 Windows 環境中執行：  
  
-   Windows 8 和 8.1  
-   Windows 10  
-   Windows Server 2012 和 2012 R2
-   Windows Server 2016
  
## <a name="database-prerequisites"></a>資料庫必要條件  
 若要使用 Oracle CDC 服務，您必須安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client Oracle 軟體。 這是應該從 Oracle 取得的必要元件，而且必須在安裝 Oracle CDC 服務之前安裝。 此外，您也需要使用 SQL Server 安裝程式安裝 SQL Server ODBC 用戶端。  
  
 Oracle CDC 服務支援以下版本：  
  
### <a name="source-oracle-database"></a>來源 Oracle 資料庫  
  
-   Oracle Database 10g Release 2
-   Oracle Database 11g Release 1 和 Release 2
-   Oracle Database 12c 正在進行傳統安裝。 (不支援多租用戶安裝。)  
  
### <a name="target-sql-server-database"></a>目標 SQL Server 資料庫  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
## <a name="running-the-installation-program"></a>執行安裝程式  
 若要安裝 Oracle CDC 服務，請開啟您所使用之 Windows 平台 (32/64 位元) 所適用的安裝精靈，然後依照畫面上的指示進行。  
  
## <a name="uninstalling-change-data-capture-service-for-oracle-by-attunity"></a>解除安裝 Attunity Oracle Change Data Capture (CDC) 服務  
 使用 [控制台] 的 [程式和功能] 解除安裝 Oracle CDC 服務。  
  
 解除安裝 CDC 服務並不會刪除所建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 若要完全移除此工具，您必須移除 MSXDBCDC 資料庫以及您在使用之目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中所建立的特定 CDC 資料庫。  
  
 如果您從一部電腦解除安裝 CDC 服務軟體並將它安裝在另一部電腦上，您只需要提供以下定義：  
  
-   服務帳戶  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接字串和認證  
  
-   主要密碼  
  
 所有其他定義都會儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，而且可從另一部電腦上的前一個安裝來使用。  
  
## <a name="in-this-documentation"></a>在此文件集中  
  
-   [Attunity Oracle Change Data Capture (CDC) 服務系統架構](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-system-architecture.md)  
  
-   [Oracle CDC 服務](../../integration-services/change-data-capture/the-oracle-cdc-service.md)  
  
-   [Attunity 的 Oracle 變更資料擷取 (CDC) 服務 F1 說明](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-f1-help.md)  
  
-   [Attunity Oracle Change Data Capture (CDC) 服務使用說明指南](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-how-to-guide.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用 Oracle CDC 服務](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
  
