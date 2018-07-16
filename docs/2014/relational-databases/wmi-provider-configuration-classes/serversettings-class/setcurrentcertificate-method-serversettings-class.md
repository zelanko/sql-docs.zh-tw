---
title: SetCurrentCertificate 方法 （ServerSettings 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SetCurrentCertificate Method (ServerSettings Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: f9c6e172-11be-42de-b19b-a5b3436e84da
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a31c59172d7c9928dd46aa24a0d876bd6df9a2a1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315910"
---
# <a name="setcurrentcertificate-method-serversettings-class"></a>SetCurrentCertificate 方法 (ServerSettings 類別)
  設定目前的安全性憑證。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.SetCurrentCertificate(  
SHA  
)  
  
```  
  
## <a name="parts"></a>組件  
 *object*  
 [ServerSettings 類別] serversettings-class.md) 物件，表示伺服器設定的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
#### <a name="parameters"></a>參數  
  
|參數|描述|  
|---------------|-----------------|  
|*SHA*|指定目前安全性憑證的字串值。|  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 `uint32` 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
