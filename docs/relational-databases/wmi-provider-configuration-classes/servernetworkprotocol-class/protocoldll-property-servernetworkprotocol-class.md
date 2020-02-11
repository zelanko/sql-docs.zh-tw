---
title: ProtocolDLL 屬性（ServerNetworkProtocol）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolDLL Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolDLL property
ms.assetid: ac386558-392e-46f3-97f8-382f267b7fca
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3cbf2d7968f1e0af97cf28604768b01fb27511cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73659437"
---
# <a name="protocoldll-property-servernetworkprotocol-class"></a>ProtocolDLL 屬性 (ServerNetworkProtocol 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得伺服器網路通訊協定所需的 .dll 檔案名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>組件  
 *目標*  
 代表實例所使用之[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]網路通訊協定的[ServerNetworkProtocol 類別](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md)物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定伺服器網路通訊協定所需之通訊協定 .dll 檔案的字串值。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定與網路程式庫](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
