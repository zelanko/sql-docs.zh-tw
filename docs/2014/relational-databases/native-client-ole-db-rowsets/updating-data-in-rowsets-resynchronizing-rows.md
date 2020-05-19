---
title: 重新同步處理資料列 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
ms.assetid: d2d30505-a878-4aa9-b821-53d8118a45a5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 39579347453fd7e40e4d8c03fe2ebb8eca3fe5a9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704726"
---
# <a name="resynchronizing-rows"></a>重新同步處理資料列
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者只支援資料指標支援的資料列集上的**IRowsetResynch** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 **IRowsetResynch** 無法視需要提供。 取用者必須在開啟資料列集前要求此介面。  
  
## <a name="see-also"></a>另請參閱  
 [更新資料列集內的資料](updating-data-in-rowsets.md)  
  
  
