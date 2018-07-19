---
title: 啟用屬性 （ServerNetworkProtocol 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Enabled Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Enabled property
ms.assetid: a514822a-91f1-4aca-9175-2b96cff29700
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0eab01e4ccc8eb0521186304be114264b951617f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278774"
---
# <a name="enabled-property-servernetworkprotocol-class"></a>Enabled 屬性 (ServerNetworkProtocol 類別)
  取得布林屬性，該屬性會指定是否啟用伺服器網路通訊協定。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.Enabled [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 A [ServerNetworkProtocol 類別](servernetworkprotocol-class.md)物件，表示執行個體所使用的網路通訊協定[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定是否啟用伺服器網路通訊協定的布林值：如果要啟用伺服器網路通訊協定為 `true`，如果要停用伺服器網路通訊協定則為 `false`。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
