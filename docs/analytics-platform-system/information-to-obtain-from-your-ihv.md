---
title: 若要從您 IHV (Analytics Platform System) 取得的資訊
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bce301a-704c-4236-a0a1-851bd17e2b6c
caps.latest.revision: 11
ms.openlocfilehash: 384a4051df1596dc334a78a751cb7954f512e8d5
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="information-to-obtain-from-your-ihv"></a>若要從您 IHV 取得的資訊
當您獨立硬體廠商 (IHV) 傳遞至您的新的 SQL Server PDW 應用裝置時，它們也提供它們對您的應用裝置上的應用裝置的硬體和設定資訊。 您將需要這項資訊來管理您的應用裝置。  
  
下列清單顯示您 IHV 通常所需的資訊。 在某些情況下，您需要額外或其他資訊。 請洽詢您 IHV 以確定應用裝置傳遞所有的相關資訊傳送給您。  
  
|||  
|-|-|  
|**資訊或文件**|**說明**|  
|用料表 (BOM)|帳單的料表會列出您的應用裝置中包含的元件。 這項資訊是為了確認已傳遞的所有元件。<br /><br />**重要事項：**您材料應包含加權，針對每個應用裝置節點和每個完整的機架。 這項資訊，請務必在規劃如何處理及移動應用裝置的管線元件，並確定您的資料中心可以容納應用裝置。 如果您 BOM 不包含節點加權，請務必從您的所有節點 IHV 取得這項資訊。|  
|纜線圖表|纜線圖表會顯示如何在網路、 強大功能及其他每個應用裝置的纜線連接機架。 每當您需要移除或取代元件還安裝，在資料中心內的應用裝置時需要這些圖表。|  
|應用裝置軌道需求|您的應用裝置可以安裝在您的資料中心之前，您需要知道您的資料中心是否符合氣流應用裝置，以及大小的纜線長度需求和電源需求的元件。 另請參閱的用料表 (BOM) 上述有關應用裝置元件的加權值，也是必要。|  
  
