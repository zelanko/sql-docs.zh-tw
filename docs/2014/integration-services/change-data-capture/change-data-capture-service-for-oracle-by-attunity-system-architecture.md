---
title: Attunity Oracle 異動資料擷取服務系統架構 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1db6c737-3c60-4066-a0a3-3611e1c83e4e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 84ac0e6065fa3fb4845e0e3a47ce56816705e80d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389396"
---
# <a name="change-data-capture-service-for-oracle-by-attunity-system-architecture"></a>Attunity Oracle Change Data Capture (CDC) 服務系統架構
  Oracle CDC 服務會將一個或多個來源 Oracle 資料庫中選定資料表所做的變更擷取到位於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC 資料庫中。 下圖顯示組成 Oracle CDC 服務的元件。  
  
 ![服務架構](../media/service-architecture.gif "服務架構")  
  
 這個圖說明使用的四個平台。 在許多情況下，這些平台可以重疊，但是這個圖代表標準使用情況。 例如，以下是合理的情況：Oracle 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫各自在不同的電腦上執行，而且不與 Oracle CDC 服務平台或是設計 CDC 服務所使用的平台共用。 此圖所說明的平台如下：  
  
-   Oracle CDC 服務：這可以是任何支援的 Windows 電腦已安裝並執行 Oracle CDC 服務的所在。 這個平台也可能代表 Microsoft 容錯移轉叢集中的叢集節點 (本文稍後會討論高可用性組態)。  
  
-   Oracle 資料庫：這可以是任何支援的 Oracle 資料庫版本的執行所在的電腦。 其中包括執行 Windows、Linux 或是安裝之 Oracle 資料庫版本所支援的任何其他作業系統的電腦。 請注意，此圖以複數形式顯示這個平台，因為單一 Oracle CDC 服務可以從多個來源 Oracle 資料庫擷取變更。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:這可以是任何電腦，目標[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫 (支援的 SKU 的[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]) 執行。 Oracle CDC 服務支援一個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 目標，它會將變更資料表和服務組態儲存在此目標上。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 平台也可能代表 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 的叢集執行個體，或是使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] AlwaysOn **功能的** 鏡像執行個體。  
  
-   Oracle CDC 設計工具：這可以是任何支援的 Windows 電腦可存取來源 Oracle 資料庫和目標[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫。  
  
 下表描述在上述四個平台上執行的元件。  
  
|元件/描述|元件的組成項目：|  
|----------------------------|----------------------------|  
|Oracle CDC 服務：這是 Windows 服務變更資料擷取活動發生的地方。|Oracle CDC 執行個體：處理變更資料擷取活動 （沒有每個來源 Oracle 資料庫的一個 Oracle CDC 執行個體） 的單一來源 Oracle 資料庫的 Oracle CDC 服務的子處理序。<br /><br /> Oracle 記錄讀取器：讀取 Oracle 交易記錄使用 Oracle 用戶端。<br /><br /> Oracle 用戶端：用來與 Oracle 通訊之 Oracle Instant Client。 這是應該從 Oracle 取得的必要元件，而且必須在安裝 Oracle CDC 服務之前安裝。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 變更寫入器：這對擷取的 Oracle 資料表所做的認可的變更寫入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]變更資料表。 此元件也會在目標 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中維護該擷取狀態。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ODBC 用戶端：適用於 Microsoft 原生用戶端[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。 這是應該從 Microsoft 取得的必要元件，而且必須在安裝 Oracle CDC 服務之前安裝。|  
|Oracle CDC 服務組態：這是 Microsoft Management Console 嵌入式管理單元，會建立 Windows 服務，並設定其組態。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端：隨附於.NET framework 第 4 版的 SQL ADO.NET 用戶端。|  
|Oracle 資料庫：若要選取資料表的變更從來源 Oracle 資料庫擷取。|記錄採礦器：透過此讀取 Oracle 交易記錄的 Oracle 元件。<br /><br /> 交易記錄檔：線上和封存 Oracle 重做記錄，oracle 可確保資料庫可以回復交易，並從 （在此情況下，Oracle 資料庫必須在封存記錄模式中運作） 的失敗中復原。|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體：A [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC 資料庫的裝載位置的執行個體。 這可能是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 叢集執行個體 (容錯移轉叢集) 或鏡像資料庫 (AlwaysOn)。|MSXDBCDC 資料庫：資料庫，以此方式運作之 CDC 服務的相關資訊[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]保留執行個體。 它也會保存有關每一個 CDC 服務所處理之 Oracle CDC 執行個體的資訊。 這個資料庫會在建立 CDC 服務的過程中建立。<br /><br /> CDC 資料庫：儲存其中一個來源 Oracle 資料庫所做之變更的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫。 CDC 資料庫會啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC，好讓這些資料庫擁有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC 資料表和函數，如此便可輕鬆地取用來自 Oracle 的變更。|  
|Oracle CDC 設計工具：Microsoft Management Console 嵌入式管理單元，可協助建立 Oracle CDC 執行個體。 使用這個項目來選取要擷取的資料表和資料行、提供 Oracle 連接資訊及管理 CDC 執行個體的生命週期。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端：隨附於.NET framework 第 4 版的 SQL ADO.NET 用戶端。<br /><br /> Oracle 用戶端：用來與 Oracle 通訊之 Oracle Instant Client。 這是應該從 Oracle 取得的必要元件，而且必須在安裝 Oracle CDC 服務之前安裝。|  
  
 Oracle CDC 服務和其子項 Oracle CDC 執行個體只能與來源 Oracle 資料庫及當做用戶端的目標 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體通訊。 它們不會主動接聽任何網路或其他通訊協定。 Oracle CDC 服務會監控 CDC 資料庫中的組態變更，並根據更新的組態更新其作業。  
  
  
