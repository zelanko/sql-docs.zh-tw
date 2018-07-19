---
title: 從 IHV-Analytics Platform System 取得資訊 |Microsoft 文件
description: 若要取得從您 IHV Analytics Platform System 應用裝置的相關資訊。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 57b61ed7741bc6d36b7531a62416893e7cc10fb7
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538898"
---
# <a name="information-to-obtain-from-your-ihv"></a>若要從您 IHV 取得的資訊
當您獨立硬體廠商 (IHV) 傳遞至您的新的 SQL Server PDW 應用裝置時，它們也提供它們對您的應用裝置上的應用裝置的硬體和設定資訊。 您將需要這項資訊來管理您的應用裝置。  
  
下列清單顯示您 IHV 通常所需的資訊。 在某些情況下，您需要額外或其他資訊。 請洽詢您 IHV 以確定應用裝置傳遞所有的相關資訊傳送給您。  
  
|||  
|-|-|  
|**資訊或文件**|**說明**|  
|用料表 (BOM)|帳單的料表會列出您的應用裝置中包含的元件。 這項資訊是為了確認已傳遞的所有元件。<br /><br />**重要事項：** 您材料應包含加權，針對每個應用裝置節點和每個完整的機架。 這項資訊，請務必在規劃如何處理及移動應用裝置的管線元件，並確定您的資料中心可以容納應用裝置。 如果您 BOM 不包含節點加權，請務必從您的所有節點 IHV 取得這項資訊。|  
|纜線圖表|纜線圖表會顯示如何在網路、 強大功能及其他每個應用裝置的纜線連接機架。 每當您需要移除或取代元件還安裝，在資料中心內的應用裝置時需要這些圖表。|  
|應用裝置軌道需求|您的應用裝置可以安裝在您的資料中心之前，您需要知道您的資料中心是否符合氣流應用裝置，以及大小的纜線長度需求和電源需求的元件。 另請參閱的用料表 (BOM) 上述有關應用裝置元件的加權值，也是必要。|  
  
