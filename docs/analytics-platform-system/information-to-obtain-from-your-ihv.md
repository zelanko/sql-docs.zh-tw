---
title: 從 IHV 取得資訊
description: 要從您的 IHV 取得有關分析平臺系統裝置的資訊。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 730cf09ab7e45ea74070db591592fdb871243a77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401061"
---
# <a name="information-to-obtain-from-your-ihv"></a>要從您的 IHV 取得的資訊
當您的獨立硬體廠商（IHV）將您的新 SQL Server PDW 設備提供給您時，他們也會提供設備硬體的相關資訊，以及在設備上執行的設定。 您將需要此資訊來管理您的應用裝置。  
  
下列清單顯示您的 IHV 通常需要的資訊。 在某些情況下，需要其他或其他資訊。 請洽詢您的 IHV，確保所有相關資訊都已透過設備傳遞傳送給您。  
  
|||  
|-|-|  
|**資訊或檔**|**說明**|  
|物料清單（BOM）|您的物料清單會列出設備中包含的元件。 這是確認已傳遞所有元件所需的資訊。<br /><br />**重要事項：** 您的物料清單應該包含每個設備節點的權數，以及每個完整機架的權數。 當您規劃如何處理和行動裝置元件，以及確保您的資料中心可以容納設備時，這項資訊非常重要。 如果您的 BOM 不包含節點加權，請務必從您的 IHV 針對所有節點取得此資訊。|  
|纜線圖|纜線圖顯示如何連接每個設備機架的網路、電源和其他纜線。 在您的資料中心安裝設備時，以及任何需要移除或更換元件時，都需要這些圖表。|  
|設備機架需求|您必須先知道您的資料中心是否符合設備的氣流和纜線長度需求，以及元件的大小和電源需求，才能將設備安裝在您的資料中心。 如需設備元件權數（也是必要）的相關資訊，請參閱上方的材料物料單（BOM）。|  
  
