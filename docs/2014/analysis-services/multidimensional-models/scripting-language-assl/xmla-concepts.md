---
title: XMLA 概念 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XMLA, concepts
ms.assetid: 816183a7-d2f7-4e14-8e5b-2a4c1798fbc1
author: minewiskan
ms.author: owend
ms.openlocfilehash: b2e18917b56d40f8b813ba10083cc1b408e51a98
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545650"
---
# <a name="xmla-concepts"></a>XMLA 概念
  XML for Analysis (XMLA) 開放標準支援對位於全球資訊網上的資料來源進行資料存取。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 根據 xmla 1.1 規格來執行 xmla。  
  
 XML for Analysis (XMLA) 是以簡易物件存取通訊協定 (SOAP) 為基礎的 XML 通訊協定，它是特別針對位在網路上的任何標準多維度資料來源進行通用資料存取而設計。 XMLA 也不需要部署會公開元件物件模型（COM）或 .NET Framework 介面的用戶端元件 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。 XMLA 是針對網際網路最佳化，因為在這種環境下，往返伺服器的作業會耗用大量的時間和資源，而且資料來源的可設定狀態連接可能會限制伺服器上的使用者連接。  
  
 XMLA 是的原生通訊協定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ，用於用戶端應用程式和實例之間的所有互動 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 完全支援 XML for Analysis 1.1，而且也提供延伸模組以支援中繼資料管理、工作階段管理以及鎖定功能。 分析管理物件 (AMO) 與 ADOMD.NET 在與 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體通訊時，會使用 XMLA 通訊協定。  
  
## <a name="handling-xmla-communications"></a>處理 XMLA 通訊  
 XMLA 開放標準描述兩種普遍可存取的方法：`Discover` 與 `Execute`。 這些方法使用 XML 支援的鬆散偶合的用戶端與伺服器架構，以處理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體的傳入和傳出資訊。  
  
 `Discover` 方法可從 Web 服務取得資訊與中繼資料。 這個資訊可包括可用資料來源的清單，以及有關任何資料來源提供者的資訊。 屬性會定義和塑造從資料來源取得的資料。 用戶端應用程式可能會需要來自 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體資料來源的許多資訊，`Discover` 方法正是定義這些資訊類型的常見方法。 屬性與泛型介面提供的擴充性，讓您不需要在用戶端應用程式中重新撰寫已有的函數。  
  
 `Execute` 方法可讓應用程式針對 XMLA 資料來源執行提供者特定的命令。  
  
 雖然 XMLA 通訊協定是針對 Web 應用程式最佳化，它也可以供 LAN 導向的應用程式使用。 下列應用程式可以從這個以 XML 為基礎的 API 獲益：  
  
-   在用戶端與伺服器之間需要彈性技術的用戶端/伺服器應用程式  
  
-   以多個作業系統為目標的用戶端/伺服器應用程式  
  
-   不需要重要狀態以增加伺服器容量的用戶端  
  
## <a name="xmla-and-the-unified-dimensional-model"></a>XMLA 與統一維度模型  
 XMLA 是運用統一維度模型 (UDM) 方法的商業智慧應用程式所使用的通訊協定。  
  
  
