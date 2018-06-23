---
title: SetFlag 方法 （ServerNetworkProtocolProperty 類別） |Microsoft 文件
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
- SetFlag Method (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetFlag method
ms.assetid: 95288931-8eb1-4477-ad80-619cf7073e61
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 285e00e7f4f8c7b640523d76f9bd9dc96f68d4e1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134895"
---
# <a name="setflag-method-servernetworkprotocolproperty-class"></a>SetFlag 方法 (ServerNetworkProtocolProperty 類別)
  設定參考之屬性的旗標。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetFlag(  
BoolValue  
)  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 [ServerNetworkProtocolProperty 類別] servernetworkprotocolproperty-class.md) 表示的執行個體上網路通訊協定的屬性物件[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*BoolValue*|指定旗標之新值的布林值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  