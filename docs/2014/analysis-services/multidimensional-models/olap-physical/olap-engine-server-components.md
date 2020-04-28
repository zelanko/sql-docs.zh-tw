---
title: OLAP 引擎伺服器元件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services, architecture
- ports [Analysis Services]
- XML/A listener
- server architecture [Analysis Services]
ms.assetid: 5193c976-9dcd-459c-abba-8c3c44e7a7f2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 535d1e05fc82882e0a2b5ea43ac9b2147e62338b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388012"
---
# <a name="olap-engine-server-components"></a>OLAP 引擎伺服器元件
  的[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]伺服器元件是以 Windows 服務形式執行的**msmdsrv.exe**應用程式。 這個應用程式是由安全性元件、XML for Analysis (XMLA) 接聽程式元件、查詢處理器元件及執行下列功能的許多其他內部元件所組成：

-   剖析從用戶端收到的陳述式

-   管理中繼資料

-   處理交易

-   處理計算

-   儲存維度和資料格資料

-   建立彙總

-   排程查詢

-   快取物件

-   管理伺服器資源

## <a name="architectural-diagram"></a>架構圖表
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體會當做獨立服務來執行，並與透過 XML for Analysis (XMLA) 所進行的服務通訊 (使用 HTTP 或 TCP)。 AMO 是使用者應用程式與 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體之間的一層。 這一層提供了對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 管理物件的存取。 AMO 是一個類別庫，它會接收來自用戶端應用程式的命令，並將這些命令轉換成 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體的 XMLA 訊息。 AMO 會使用執行命令的方法成員以及為 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 物件保存資料的屬性成員，將 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體物件當做類別呈現給使用者應用程式。

 下圖顯示 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 元件架構，其中包括在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體內執行的所有主要元素以及與此執行個體互動的所有使用者元件。 下圖也會顯示存取此執行個體的唯一方法，就是使用 XML for Analysis (XMLA) 接聽程式 (利用 HTTP 或 TCP)。

 ![Analysis Services 系統架構圖表](../../../analysis-services/dev-guide/media/analysisservicessystemarchitecture.gif "Analysis Services 系統架構圖表")

## <a name="xmla-listener"></a>XMLA 接聽程式
 XMLA 接聽程式元件會處理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 及其用戶端之間的所有 XMLA 通訊。 Msmdsrv.exe [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] `Port`中的設定可以用來指定[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]實例接聽的通訊埠。 這個檔案中 0 的值表示 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會接聽預設通訊埠。 除非另有指定，否則 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會使用下列預設 TCP 通訊埠：

|連接埠|描述|
|----------|-----------------|
|2383|的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]預設實例。|
|2382|其他實例的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]重新導向程式。|
|在伺服器啟動時動態指派|的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]命名實例。|

 如需詳細資訊，請參閱[設定 Windows 防火牆以允許 Analysis Services 存取](../../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。

## <a name="see-also"></a>另請參閱
 [物件命名規則 &#40;Analysis Services&#41;](object-naming-rules-analysis-services.md) [實體架構 &#40;Analysis Services-多維度資料](understanding-microsoft-olap-physical-architecture.md)&#41;[邏輯架構 &#40;Analysis Services 多維度資料&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)


