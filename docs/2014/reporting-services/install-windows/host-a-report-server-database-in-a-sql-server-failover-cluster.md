---
title: 在 SQL Server 容錯移轉叢集中裝載報表伺服器資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 7bd5f019-2857-452f-a023-cc3b9e93aec4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a0187e58076110644928e9b06c99cb33ea73c2f0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63064462"
---
# <a name="host-a-report-server-database-in-a-sql-server-failover-cluster"></a>在 SQL Server 容錯移轉叢集中裝載報表伺服器資料庫
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供容錯移轉叢集支援，可讓您針對一或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體使用多個磁碟。 只有報表伺服器資料庫才支援容錯移轉叢集。您無法將報表伺服器服務當做容錯移轉叢集的一部分執行。  
  
 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集上主控報表伺服器資料庫，必須已經安裝及設定該叢集。 然後，在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具的 [資料庫安裝] 頁面中建立報表伺服器資料庫時，您就可以選取容錯移轉叢集當做伺服器名稱。  
  
 雖然報表伺服器服務無法參與容錯移轉叢集，但是您可以在已安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 容錯移轉叢集的電腦上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 報表伺服器的執行與容錯移轉叢集無關。 如果您在屬於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉執行個體之一部分的電腦上安裝報表伺服器，就不需要針對報表伺服器資料庫使用容錯移轉叢集。您可以使用不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來主控此資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器資料庫 &#40;SSRS 原生模式&#41;](../report-server/report-server-database-ssrs-native-mode.md)   
 [建立報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
  
  
