---
title: 資料指標類型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d88b48c1fc4166b32821da9cdaaa5eb7f6c2e60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63070995"
---
# <a name="cursor-types"></a>資料指標類型
  ODBC 會定義 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 NATIVE Client ODBC 驅動程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所支援的四種資料指標類型。 這些資料指標在偵測結果集變更的能力和其所耗用的資源（例如**tempdb**中的記憶體和空間）方面有所不同。 資料指標只有在嘗試重新提取變更過的資料列時，才能偵測到這些資料列的變更；沒有方法可讓資料來源通知資料指標目前所提取的資料列已變更。 交易隔離等級也會影響資料指標偵測到並非透過該資料指標所進行之變更的能力。  
  
 以下是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所支援的四種 ODBC 資料指標類型：  
  
-   順向資料指標：此種資料指標不支援捲動，而僅支援從資料指標開頭到結尾循序提取資料列。  
  
-   當資料指標開啟時，靜態資料指標會內建于**tempdb**中。 這種資料指標一定會顯示結果集在資料指標開啟時的原貌， 而不會反映出資料的變更。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 靜態資料指標永遠是唯讀的。 因為靜態伺服器資料指標是在**tempdb**中建立為工作資料表，所以資料指標結果集的大小不能超過所允許的資料列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]大小上限。  
  
-   索引鍵集驅動的資料指標：這種資料指標開啟時，會將結果集中資料列的成員資格和順序設為固定。 您可透過此資料指標看到非索引鍵資料行的變更。  
  
-   動態資料指標是靜態資料指標的相反。 動態資料指標會反映其結果集之中變更的資料列。 每回擷取時結果集之中資料列的資料值、順序和成員均會變動。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;使用資料指標](using-cursors-odbc.md)  
  
  
