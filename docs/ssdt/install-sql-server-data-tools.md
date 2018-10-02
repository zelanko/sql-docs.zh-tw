---
title: 安裝 SQL Server Data Tools | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.package.stub
ms.assetid: 6f8616cb-9119-42c3-a9b1-936e088763e7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a847748b0f0025402da1feb794f5c441ea2a3f5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773566"
---
# <a name="install-sql-server-data-tools"></a>安裝 SQL Server Data Tools
本主題將說明如何安裝 SQL Server Data Tools。 如需 SQL Server Data Tools 的更新，請前往 SQL Server Data Tools 下載頁面 ([安裝最新版的 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714))。  
  
無論您是使用 Visual Studio 2012 還是 Visual Studio 2013，請安裝最新的 SQL Server Data Tools 更新，以取得最新的功能。  
  
## <a name="sql-server-data-tools-for-visual-studio-2013"></a>Visual Studio 2013 的 SQL Server Data Tools  
SQL Server Data Tools 隨附於 Visual Studio 2013 Express for Web、Visual Studio 2013 Express for Desktop、Visual Studio Community 2013，以及所有付費的 SKU，包括 Professional SKU 和更高版本。 在安裝 Visual Studio 2013 之後，您可以移至 [工具] -> [擴充功能和更新] -> [更新]，以了解是否有要安裝的更新。  
  
## <a name="sql-server-data-tools-for-visual-studio-2012"></a>Visual Studio 2012 的 SQL Server Data Tools  
SQL Server Data Tools 會隨附在 Visual Studio 2012 中的 Professional SKU (或更高版本) 中。 安裝 Visual Studio 2012 並安裝 2012 年 11 月 (或更新版本) 的 SQL Server Data Tools 更新後，SQL Server Data Tools 可以在有可安裝更新時進行報告。 如需詳細資訊，請參閱[檢查更新檔對話方塊](../ssdt/check-for-updates-dialog-box.md)。  
  
如果未安裝 Visual Studio 2012，SQL Server Data Tools 將安裝 Visual Studio 2012 整合殼層，並安裝 SQL Server Data Tools。  
  
## <a name="administrative-installation-point"></a>系統管理安裝點  
如果您需要在多部電腦或無法存取網際網路的電腦上安裝 SQL Server Data Tools，則可先在網路共用或實體媒體上建立系統管理安裝配置，然後從該安裝點進行安裝。  
  
若要建立安裝配置，請下載 SSDTSetup.EXE 並使用 `/layout`*location* 選項來執行它，以便在 *location*建立配置。 然後，使用者就可以從 *location*執行 SSDTSetup.Exe。  
  
若要下載 SSDTSetup.exe，請前往 [安裝 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714)，再按一下您的 Visual Studio 版本適用的連結，然後下載您的語言適用的 SSDTSetup.exe。  
  
