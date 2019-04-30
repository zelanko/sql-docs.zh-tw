---
title: 取得資訊從 IHV-Analytics Platform System |Microsoft Docs
description: 若要取得有關 Analytics Platform System appliance ihv 提供的資訊。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 57b61ed7741bc6d36b7531a62416893e7cc10fb7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150225"
---
# <a name="information-to-obtain-from-your-ihv"></a>若要取得 ihv 提供的資訊
當獨立硬體廠商 (IHV) 提供給您的新的 SQL Server PDW 應用裝置時，他們也將提供設備的硬體和組態資訊已對您的應用裝置。 您將需要這項資訊來管理您的應用裝置。  
  
下列清單顯示 ihv 提供通常需要的資訊。 在某些情況下，需要額外或其他資訊。 請先確定設備傳遞所有的相關資訊傳送到您 ihv 提供。  
  
|||  
|-|-|  
|**資訊或文件**|**說明**|  
|用料表 (BOM)|您帳單的組件會列出您的應用裝置中包含的元件。 這項資訊是為了確認已傳遞的所有元件。<br /><br />**重要：** 您的帳單的組件應該包含權數，針對每個應用裝置節點和每個完整的機架。 規劃如何處理及移動設備元件時，此資訊就很重要，並確保您的資料中心可以容納應用裝置。 如果您 BOM 不包含節點的加權，請務必取得這項資訊 ihv 提供的所有節點的項目。|  
|纜線圖表|纜線圖會顯示如何連線網路、 電源和其他的纜線，每個設備的機架。 在您的資料中心安裝應用裝置時需要這些圖表，每當您需要移除或取代的元件。|  
|設備軌道需求|您的應用裝置可以安裝在您的資料中心之前，您需要知道您的資料中心是否符合氣流和設備，以及大小的纜線長度需求和元件的電源需求。 另請參閱帳單的用料表 (BOM) 上述取得的資訊應用裝置元件的加權，這也是必要。|  
  
